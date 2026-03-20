⏱️ Amortized Analysis in Time Complexity
A single expensive operation doesn't make your algorithm slow — if it happens rarely enough. Amortized analysis reveals the TRUE cost of operations over time, not just the worst case.

📌 Table of Contents
Why Amortized Analysis Matters
The Core Idea — One Sentence
Amortized vs Other Analyses
The Classic Analogy — The Restaurant Bill
When Worst Case Lies to You
The Three Methods of Amortized Analysis
Method 1 — Aggregate Method
Method 2 — Banker's (Accounting) Method
Method 3 — Physicist's (Potential) Method
Classic Examples Deep Dive
Dynamic Array (ArrayList / Vector)
Stack with Multipop
Binary Counter
Two Pointer / Sliding Window
Hash Table Rehashing
Splay Trees
Queue Using Two Stacks
Amortized Analysis in Common DSA Patterns
How to Recognize Amortized O(1) in Interviews
Amortized vs Average — The Critical Difference
Common Misconceptions
Interview Questions Involving Amortized Analysis
How to Explain Amortized Analysis in an Interview
Practice Problems
Quick Reference Card
💡 Why Amortized Analysis Matters
text

SCENARIO:
  You're using a dynamic array (like Python's list or Java's ArrayList).
  You perform n append operations.

WORST-CASE ANALYSIS says:
  → A single append can cost O(n) (when resizing happens)
  → So n appends cost O(n) × n = O(n²)
  → ❌ THIS IS WRONG. This is a massive OVERESTIMATE.

AMORTIZED ANALYSIS says:
  → Yes, ONE append can cost O(n) — but it happens RARELY
  → Most appends cost O(1)
  → Over n operations, total work = O(n)
  → Amortized cost per append = O(n) / n = O(1)
  → ✅ THIS IS THE TRUE PICTURE.

WITHOUT amortized analysis:
  → You'd think ArrayList.add() is slow
  → You'd avoid dynamic arrays
  → You'd make worse design decisions

WITH amortized analysis:
  → You understand the TRUE cost
  → You use the right data structures confidently
  → You can explain WHY to interviewers
🎯 The Core Idea — One Sentence
text

╔══════════════════════════════════════════════════════════════╗
║                                                              ║
║  Amortized analysis finds the AVERAGE cost per operation     ║
║  over a WORST-CASE sequence of operations.                   ║
║                                                              ║
║  It's NOT about probability.                                 ║
║  It's NOT about the best case.                               ║
║  It IS about spreading the cost of expensive operations      ║
║  across all operations in the sequence.                      ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
In Even Simpler Words
text

"Some operations are expensive, but they PAY FOR THEMSELVES
 by making future operations cheap. When you average over
 the entire sequence, each operation is cheap."
⚖️ Amortized vs Other Analyses
text

┌──────────────────────────────────────────────────────────────────┐
│                    TYPES OF ANALYSIS                              │
├─────────────────┬────────────────────────────────────────────────┤
│                 │                                                │
│  BEST CASE      │  The fastest any single operation can be       │
│  Ω(1)           │  → Rarely useful                              │
│                 │  → "Under perfect conditions, how fast?"       │
│                 │                                                │
├─────────────────┼────────────────────────────────────────────────┤
│                 │                                                │
│  WORST CASE     │  The slowest any single operation can be       │
│  O(n)           │  → Often too pessimistic                      │
│                 │  → "Under the WORST condition, how slow?"      │
│                 │  → Doesn't consider that worst case may        │
│                 │    happen rarely                               │
│                 │                                                │
├─────────────────┼────────────────────────────────────────────────┤
│                 │                                                │
│  AVERAGE CASE   │  Expected cost assuming RANDOM inputs          │
│  Θ(?)           │  → Requires probability assumptions           │
│                 │  → "On AVERAGE over random inputs, how fast?"  │
│                 │  → Depends on input distribution               │
│                 │                                                │
├─────────────────┼────────────────────────────────────────────────┤
│                 │                                                │
│  AMORTIZED      │  Average cost per operation over ANY           │
│  O(1) amortized │  WORST-CASE sequence of n operations          │
│                 │  → NO probability assumptions                 │
│                 │  → GUARANTEED upper bound on total work        │
│                 │  → "Over n operations, average cost per op"    │
│                 │  → Strongest guarantee after worst-case        │
│                 │                                                │
└─────────────────┴────────────────────────────────────────────────┘
The Key Distinction Visualized
text

WORST-CASE ANALYSIS:
  Operation costs: [1, 1, 1, 1, 1, 1, 1, 8, 1, 1, 1, 1, 1, 1, 1, 16, ...]
  Worst case says: "An operation can cost O(n)" → n ops cost O(n²)
                                                     ↑ OVERESTIMATE

AMORTIZED ANALYSIS:
  Same costs:      [1, 1, 1, 1, 1, 1, 1, 8, 1, 1, 1, 1, 1, 1, 1, 16, ...]
  Total work:       1+1+1+1+1+1+1+8+1+1+1+1+1+1+1+16 = ~32
  Operations:       16
  Amortized cost:   32/16 = 2 per operation → O(1) amortized ✅
🍽️ The Classic Analogy — The Restaurant Bill
text

IMAGINE:
  You go to a restaurant every day for a month (30 days).
  
  → 29 days: You order a coffee for $3
  → 1 day: You host a birthday dinner for $150
  
  WORST-CASE ANALYSIS:
    "A single visit can cost $150"
    "30 visits could cost 30 × $150 = $4,500"  ← ABSURD overestimate
  
  AVERAGE-CASE ANALYSIS (with probability):
    "ASSUMING random visits, expected cost is about $3"
    But this assumes you WON'T always host dinner ← requires assumptions
  
  AMORTIZED ANALYSIS:
    Total cost = 29 × $3 + 1 × $150 = $87 + $150 = $237
    Amortized cost per visit = $237 / 30 = $7.90
    → GUARANTEED: over any 30 visits, you pay ~$7.90 per visit
    → No probability assumptions needed
Another Analogy — Saving for a Big Purchase
text

THE BANKER'S WAY OF THINKING:

  → Every time you do a CHEAP operation, you "save" a little extra
  → The savings go into a "bank"
  → When an EXPENSIVE operation happens, you pay from the "bank"
  → If the bank never goes negative, the amortized cost is valid

  EXAMPLE:
    Every O(1) append → you "save" $2 ($1 for the append + $1 for the bank)
    After 7 cheap appends → bank has $7
    The 8th append triggers a resize costing $8 → pay from the bank
    Bank: $7 - $8 = need just $1 more → the amortized cost is ~$2 per op

  THIS IS LITERALLY THE BANKER'S METHOD (we'll formalize it below)
🔍 When Worst Case Lies to You
The Problem with Pure Worst-Case Thinking
text

SITUATION 1: Dynamic Array Append
  → Worst case per append: O(n)
  → Worst case for n appends: O(n²)     ← LIE
  → True cost for n appends: O(n)       ← TRUTH (amortized O(1) per append)

SITUATION 2: Stack with Multipop
  → Worst case per multipop: O(n)
  → Worst case for n operations: O(n²)  ← LIE
  → True cost for n operations: O(n)    ← TRUTH (amortized O(1) per op)

SITUATION 3: Sliding Window
  → Inner while loop can iterate up to n times
  → Looks like O(n²) with outer loop     ← LIE
  → True cost: O(n)                      ← TRUTH (each element enters/exits once)

SITUATION 4: Union-Find with Path Compression + Union by Rank
  → Single Find can traverse the whole tree
  → Worst case per Find: O(n)            ← MISLEADING
  → Amortized per Find: O(α(n)) ≈ O(1)  ← TRUTH (α is inverse Ackermann)
WHY Does Worst Case Overestimate?
text

Because worst case assumes EVERY operation is maximally expensive.
But in reality:

  → An expensive operation often RESETS the state
  → After resetting, the NEXT several operations are cheap
  → The expensive operation "pays" for itself by making future ops cheap

ANALOGY:
  → A volcano erupts violently... then is quiet for decades
  → Worst-case says "it could erupt every day" ← technically true but unrealistic
  → Amortized says "over 100 years, average eruptions per year = 0.01"
🧮 The Three Methods of Amortized Analysis
text

THREE WAYS TO PROVE THE SAME THING:

  1. AGGREGATE METHOD     → "Count total work, divide by n"
  2. BANKER'S METHOD      → "Charge extra on cheap ops, save for expensive ones"
  3. PHYSICIST'S METHOD   → "Define a potential function that captures stored work"

THEY ALL GIVE THE SAME ANSWER.
Choose the one that's easiest for the specific problem.
Which Method to Use When
text

┌────────────────────┬─────────────────────────────────────────┐
│ Method             │ Best When                               │
├────────────────────┼─────────────────────────────────────────┤
│ Aggregate          │ You can directly count total work       │
│                    │ Simplest to understand                  │
│                    │ Good for: dynamic arrays, binary counter│
├────────────────────┼─────────────────────────────────────────┤
│ Banker's           │ Different operations have different     │
│ (Accounting)       │ amortized costs                        │
│                    │ Intuitive "credit" system               │
│                    │ Good for: stack multipop, splay trees   │
├────────────────────┼─────────────────────────────────────────┤
│ Physicist's        │ Complex data structure state changes    │
│ (Potential)        │ Most mathematically rigorous            │
│                    │ Good for: Fibonacci heaps, splay trees  │
│                    │ Needed for formal proofs                │
└────────────────────┴─────────────────────────────────────────┘
Method 1 — The Aggregate Method
The simplest method. Count the total work for n operations, then divide by n.

The Idea
text

STEP 1: Consider a sequence of n operations
STEP 2: Calculate the TOTAL cost of ALL n operations combined: T(n)
STEP 3: Amortized cost per operation = T(n) / n

If T(n) = O(n), then amortized cost = O(n)/n = O(1) per operation
If T(n) = O(n log n), then amortized cost = O(log n) per operation
How It Works — Dynamic Array Example
text

SETUP:
  → Dynamic array starts with capacity 1
  → When full, CREATE a new array of DOUBLE the size
  → Copy all elements to new array
  → Then insert the new element

OPERATION COSTS for n = 16 inserts:

  Insert #1:  cost = 1  (insert into empty array of size 1)
  Insert #2:  cost = 1 + 1 = 2  (resize: copy 1 element + insert)
  Insert #3:  cost = 2 + 1 = 3  (resize: copy 2 elements + insert)
  Insert #4:  cost = 1  (no resize, capacity is 4)
  Insert #5:  cost = 4 + 1 = 5  (resize: copy 4 elements + insert)
  Insert #6:  cost = 1
  Insert #7:  cost = 1
  Insert #8:  cost = 1
  Insert #9:  cost = 8 + 1 = 9  (resize: copy 8 elements + insert)
  Insert #10: cost = 1
  Insert #11: cost = 1
  Insert #12: cost = 1
  Insert #13: cost = 1
  Insert #14: cost = 1
  Insert #15: cost = 1
  Insert #16: cost = 1
  
  Visually:
  
  Cost:  1  2  3  1  5  1  1  1  9  1  1  1  1  1  1  1
  Op #:  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16
              ↑        ↑              ↑
           RESIZE   RESIZE         RESIZE
           (rare)   (rarer)        (rarest)

TOTAL COST CALCULATION:
  → Resize costs: 1 + 2 + 4 + 8 = 15  (geometric series)
  → Regular insert costs: 16 × 1 = 16
  → Total = 15 + 16 = 31

  For general n:
  → Resize costs: 1 + 2 + 4 + 8 + ... + n/2 = n - 1  (geometric series sum)
  → Regular insert costs: n
  → Total T(n) = (n - 1) + n = 2n - 1 = O(n)

AMORTIZED COST:
  → T(n) / n = O(n) / n = O(1) per insert ✅

CONCLUSION:
  → Each append is O(1) AMORTIZED
  → Even though individual appends can be O(n)
The Geometric Series Insight
text

WHY DOUBLING MAKES IT WORK:

  Resize costs form a geometric series: 1 + 2 + 4 + 8 + ... + n/2

  SUM = n - 1 ≈ n

  This is because: 1 + 2 + 4 + ... + 2^k = 2^(k+1) - 1

  THE KEY INSIGHT:
  → Each resize DOUBLES the capacity
  → So the NEXT resize is at LEAST twice as far away
  → The total resizing work is bounded by 2n
  → This is why doubling (factor 2) is the standard growth factor

  WHAT IF WE GREW BY +1 INSTEAD OF ×2?
  → Resize at every insert: 1 + 2 + 3 + ... + n = n(n+1)/2 = O(n²)
  → Amortized cost: O(n²)/n = O(n) per insert ← TERRIBLE
  → This is why ArrayList doesn't grow by +1

  WHAT IF WE GREW BY ×3 OR ×4?
  → Still O(1) amortized, but wastes more memory
  → Factor of 2 is the sweet spot between time and space
  → Some implementations use 1.5 (Java ArrayList uses ~1.5)
Method 2 — The Banker's (Accounting) Method
Assign an artificial "charge" to each operation. Overcharge cheap operations to build up "credit" for expensive ones.

The Idea
text

CONCEPT:
  → Assign an AMORTIZED COST (ĉᵢ) to each operation
  → This cost can be DIFFERENT from the actual cost (cᵢ)
  → If ĉᵢ > cᵢ → the excess is stored as CREDIT
  → If ĉᵢ < cᵢ → credit is used to pay the difference
  
RULE:
  → The total credit must NEVER go negative
  → Σ ĉᵢ ≥ Σ cᵢ for ALL prefixes of operations
  → This guarantees the amortized costs are valid upper bounds

THINK OF IT AS:
  → Every cheap operation "pays forward" for future expensive operations
  → Like paying insurance premiums — small regular payments cover rare big costs
How It Works — Dynamic Array Example
text

ASSIGN:
  → Amortized cost per insert = 3 (we'll prove this works)

FOR EACH INSERT:
  → Actual cost of insertion = 1
  → Extra credit saved = 3 - 1 = 2

  → These 2 credits are "stored" on the element itself:
    • 1 credit to copy THIS element during the next resize
    • 1 credit to copy ONE OLD element during the next resize

WHEN A RESIZE HAPPENS (at insert #n+1, array was full at n):
  → Need to copy n elements to new array
  → Cost = n (for copying) + 1 (for the new insert)
  → But we have n credits saved up (2 credits per element, 
    but only n/2 elements since last resize, so... let's trace it)

DETAILED TRACE (capacity doubles from 4 to 8):

  After inserts 1-4 (capacity = 4):
    Slot 1: [value] + 0 credits (used during resize to cap 4)
    Slot 2: [value] + 0 credits (used during resize to cap 4)
    Slot 3: [value] + 2 credits (saved since cap became 4)
    Slot 4: [value] + 2 credits (saved since cap became 4)
    Total credits = 4

  Insert 5 triggers resize (copy 4 elements + insert):
    Resize cost = 4 (copying) + 1 (insert) = 5
    Credits available = 4 (from slots 3,4) + 3 (charged for insert 5) = 7
    Credits used = 5
    Credits remaining = 2 ← enough! Never goes negative ✅

  After resize, capacity = 8:
    Now we charge 3 per insert for inserts 6, 7, 8
    Each builds up credits for the NEXT resize at insert 9

THE MATH WORKS OUT:
  → Amortized cost = 3 per operation
  → Credit never goes negative
  → Therefore, total cost ≤ 3n = O(n)
  → Amortized per operation = O(1) ✅
The Credit Visualization
text

IMAGINE each element carries a little "wallet" of credits:

  INSERT 1 (no resize):
    [elem1 💰💰]     charge: 3, actual: 1, saved: 2
    
  INSERT 2 (resize from 1→2):
    [elem1] [elem2 💰💰]   resize cost: 1+1=2, credits from elem1: 2, 
                            net: 0, new element saves 2

  INSERT 3 (resize from 2→4):
    [elem1] [elem2] [elem3 💰💰]  resize cost: 2+1=3, 
                                    credits from elem2: 2, charge: 3
                                    net: 2+3-3=2 saved on elem3

  And so on... credits always cover the resize cost
Method 3 — The Physicist's (Potential) Method
Define a "potential function" Φ that measures the "stored energy" in the data structure. Expensive operations decrease potential; cheap operations increase it.

The Idea
text

DEFINE:
  → Φ(Dᵢ) = potential after the i-th operation
  → Φ(D₀) = initial potential (usually 0)
  → cᵢ = actual cost of operation i
  → ĉᵢ = amortized cost of operation i

FORMULA:
  ĉᵢ = cᵢ + Φ(Dᵢ) - Φ(Dᵢ₋₁)

  Amortized cost = Actual cost + Change in potential

TOTAL AMORTIZED COST:
  Σ ĉᵢ = Σ cᵢ + Φ(Dₙ) - Φ(D₀)

RULE:
  → If Φ(Dₙ) ≥ Φ(D₀), then Σ ĉᵢ ≥ Σ cᵢ
  → The amortized total is an UPPER BOUND on actual total ✅

INTUITION:
  → Potential = "stored energy" or "debt" in the data structure
  → When you do cheap work → potential increases (storing energy)
  → When you do expensive work → potential decreases (releasing energy)
  → The potential "absorbs" the cost spikes
How It Works — Dynamic Array Example
text

DEFINE POTENTIAL:
  Φ(D) = 2 × (size - capacity/2)
  
  WHERE:
    size = number of elements currently in the array
    capacity = current allocated capacity

  INTUITION:
    → Right after a resize, size = capacity/2 + 1, so Φ ≈ 2
    → Right before a resize, size = capacity, so Φ = 2 × (capacity/2) = capacity
    → The potential is HIGHEST right before a resize (lots of stored energy)
    → The potential DROPS after a resize (energy was used)

CASE 1: Insert WITHOUT resize (size < capacity)
  → cᵢ = 1 (just insert)
  → Φ increases by 2 (size goes up by 1 → 2×1 = 2 increase)
  → ĉᵢ = 1 + 2 = 3

CASE 2: Insert WITH resize (size = capacity, new capacity = 2 × old)
  → cᵢ = size + 1 (copy all elements + insert)
  → Old Φ = 2 × (capacity - capacity/2) = capacity
  → New Φ = 2 × ((capacity + 1) - (2×capacity)/2) = 2 × 1 = 2
  → ΔΦ = 2 - capacity
  → ĉᵢ = (capacity + 1) + (2 - capacity) = 3

IN BOTH CASES: ĉᵢ = 3 = O(1) ✅

THE BEAUTY:
  → The potential function AUTOMATICALLY balances everything
  → Expensive operations cause a BIG DROP in potential
  → The drop EXACTLY offsets the high actual cost
  → Result: constant amortized cost regardless of which case
Potential Method Intuition
text

THINK OF IT LIKE A SPRING:

  ┌─────────────────────────────────────────┐
  │                                         │
  │  Compressed spring = HIGH potential     │
  │  (many elements, near capacity)         │
  │  Ready to "explode" (resize)            │
  │                                         │
  │  Released spring = LOW potential        │
  │  (just resized, lots of empty space)    │
  │  Will take many inserts to compress     │
  │  again                                  │
  │                                         │
  │  Each insert COMPRESSES the spring a    │
  │  little (increases potential)           │
  │                                         │
  │  A resize RELEASES the spring           │
  │  (decreases potential dramatically)     │
  │                                         │
  │  The energy released PAYS for the       │
  │  resize cost                            │
  │                                         │
  └─────────────────────────────────────────┘
Comparing the Three Methods
text

                    ┌─────────────────────────────────────────────────┐
                    │           SAME PROBLEM, THREE LENSES            │
                    ├─────────────────────────────────────────────────┤
                    │                                                 │
AGGREGATE:          │  "Total work for n inserts = O(n)"             │
  (The Accountant)  │  "Amortized = O(n)/n = O(1)"                  │
  Simplest.         │  Just count everything up and divide.          │
                    │                                                 │
BANKER'S:           │  "Charge $3 per insert, save $2 as credit"    │
  (The Banker)      │  "Credit pays for resize when it happens"     │
  Most intuitive.   │  Credits never go negative → valid.           │
                    │                                                 │
PHYSICIST'S:        │  "Φ = 2(size - cap/2)"                        │
  (The Physicist)   │  "ĉᵢ = cᵢ + ΔΦ = 3 in all cases"            │
  Most rigorous.    │  Potential absorbs cost spikes.                │
                    │                                                 │
                    │  ALL THREE → Amortized O(1) per insert ✅      │
                    └─────────────────────────────────────────────────┘
🔬 Classic Examples Deep Dive
Example 1 — Dynamic Array (ArrayList / Vector)
text

OPERATIONS: n append operations
WORST CASE PER OPERATION: O(n) — when resizing
AMORTIZED PER OPERATION: O(1)

WHY:
  → Array doubles in size when full
  → Resize at sizes: 1, 2, 4, 8, 16, 32, ...
  → Resize costs: 1 + 2 + 4 + 8 + ... + n/2 < n
  → Total work: n (inserts) + n (resize copies) = 2n = O(n)
  → Amortized: O(n)/n = O(1)

THE KEY INSIGHT:
  → Doubling means each element is copied at most O(log n) times
    over its lifetime
  → But summing over all elements, total copies = O(n)
  → The geometric series converges!

  Copies of element at position k:
    → Element at position 1: copied ⌊log n⌋ times
    → Element at position n/2: copied 1 time
    → Element at position n: copied 0 times
    → Total: Σ from i=0 to log n of (n/2^i) = O(n)

REAL-WORLD APPLICATIONS:
  → Python list.append()
  → Java ArrayList.add()
  → C++ vector.push_back()
  → JavaScript Array.push()
  → ALL use this amortized O(1) principle
Example 2 — Stack with Multipop
text

OPERATIONS:
  → PUSH(x): Push element onto stack — costs O(1)
  → POP(): Pop one element — costs O(1)
  → MULTIPOP(k): Pop min(k, stack_size) elements — costs O(min(k, n))

THE WORRY:
  → MULTIPOP can cost O(n) in the worst case
  → n operations could include many MULTIPOPs
  → Worst-case analysis: n operations × O(n) each = O(n²)  ← OVERESTIMATE

AGGREGATE ANALYSIS:
  → Each element can be PUSHED at most once
  → Each element can be POPPED at most once
  → (you can't pop something that wasn't pushed)
  → So total POPs across ALL operations ≤ total PUSHes ≤ n
  → Total work ≤ n (pushes) + n (pops) = 2n = O(n)
  → Amortized per operation = O(1)

THE KEY INSIGHT:
  → MULTIPOP can be expensive, but ONLY if lots of 
    elements were previously pushed cheaply
  → The pushes "pay for" the future pops
  → Total pops can NEVER exceed total pushes

BANKER'S METHOD:
  → Charge 2 for each PUSH (1 for the push + 1 saved for future pop)
  → Charge 0 for each POP/MULTIPOP (paid from saved credits)
  → Credits never go negative (can't pop what wasn't pushed)
  → Amortized cost of PUSH = 2 = O(1)
  → Amortized cost of POP/MULTIPOP = 0 = O(1)

VISUALIZATION:
  PUSH A:  [A💰]                    charge: 2, actual: 1, credit: 1
  PUSH B:  [A💰][B💰]              charge: 2, actual: 1, credit: 2
  PUSH C:  [A💰][B💰][C💰]        charge: 2, actual: 1, credit: 3
  MULTIPOP(3): []                   charge: 0, actual: 3, credit: 3→0 ✅
Example 3 — Binary Counter
text

SETUP:
  → An array of k bits representing a binary number
  → INCREMENT operation: add 1 to the counter
  → Start from 0, perform n increments

OPERATION COST:
  → Cost = number of BITS FLIPPED in each increment

TRACE:
  Counter Value → Binary → Bits Flipped
  0 → 00000 →     -
  1 → 00001 →     1  (flip bit 0)
  2 → 00010 →     2  (flip bit 0 and bit 1)
  3 → 00011 →     1  (flip bit 0)
  4 → 00100 →     3  (flip bits 0, 1, 2)
  5 → 00101 →     1  (flip bit 0)
  6 → 00110 →     2  (flip bits 0, 1)
  7 → 00111 →     1  (flip bit 0)
  8 → 01000 →     4  (flip bits 0, 1, 2, 3)
  
  Bit flips:  1  2  1  3  1  2  1  4  1  2  1  3  1  2  1  5  ...

WORST CASE PER INCREMENT: O(k) bits flipped (all bits flip)
WORST CASE FOR n INCREMENTS: O(n × k)  ← OVERESTIMATE

AGGREGATE ANALYSIS:
  → How often does each bit flip?
  
  Bit 0 (rightmost): flips EVERY increment → n times
  Bit 1:             flips every 2nd increment → n/2 times
  Bit 2:             flips every 4th increment → n/4 times
  Bit 3:             flips every 8th increment → n/8 times
  ...
  Bit j:             flips every 2ʲ-th increment → n/2ʲ times

  Total flips = n + n/2 + n/4 + n/8 + ...
              = n × (1 + 1/2 + 1/4 + 1/8 + ...)
              = n × 2
              = 2n
              = O(n)

  Amortized cost per increment = O(n)/n = O(1)

EVEN THOUGH individual increments can flip O(k) bits,
the AMORTIZED cost is O(1) per increment!

THE PATTERN:
  → The most frequently flipping bit is the cheapest (bit 0: O(1))
  → The most expensive flips (many bits) happen EXPONENTIALLY less often
  → The geometric series saves us: 1 + 1/2 + 1/4 + ... = 2
Example 4 — Two Pointer / Sliding Window
text

THIS IS AMORTIZED ANALYSIS IN DISGUISE!

PROBLEM: 
  Find the longest subarray with sum ≤ K

APPROACH:
  → Outer loop: right pointer moves from 0 to n-1
  → Inner loop: left pointer moves right while sum > K

THE WORRY:
  → The inner while loop could run up to n times
  → Nested loops → O(n²)?  ← WRONG!

AMORTIZED ANALYSIS:
  → The RIGHT pointer moves RIGHT n times total
  → The LEFT pointer moves RIGHT at most n times total
  → Left pointer NEVER moves backward
  → Total pointer movements = n + n = 2n = O(n)
  → Amortized cost per iteration of outer loop = O(1)

VISUALIZATION:

  Array: [ 2  1  5  3  2  4  1  3 ]  Target sum ≤ 7

  right=0: [2]               left=0, sum=2 ≤ 7 ✅
  right=1: [2,1]             left=0, sum=3 ≤ 7 ✅
  right=2: [2,1,5]           left=0, sum=8 > 7
            [1,5]            left=1, sum=6 ≤ 7 ✅
  right=3: [1,5,3]           left=1, sum=9 > 7
            [5,3]            left=2, sum=8 > 7
            [3]              left=3, sum=3 ≤ 7 ✅
  right=4: [3,2]             left=3, sum=5 ≤ 7 ✅
  ...

  Left pointer moved:  0→0→0→1→1→2→3→3→... 
  It only moves RIGHT, never LEFT.
  Over ALL iterations, left moves at most n times.

THIS IS WHY SLIDING WINDOW IS O(n), NOT O(n²):
  → It's amortized O(1) per step
  → Even though the inner loop CAN run many times in a single step
  → Over ALL steps, total inner iterations ≤ n
Example 5 — Hash Table Rehashing
text

SETUP:
  → Hash table with load factor threshold α (typically 0.75)
  → When load factor exceeds α → REHASH (double table size, reinsert all)

WORST CASE PER INSERT: O(n) — when rehashing
AMORTIZED PER INSERT: O(1)

ANALYSIS (same as dynamic array):
  → Rehash at sizes: 1, 2, 4, 8, 16, 32, ...
  → Rehash costs: 1 + 2 + 4 + 8 + ... + n/2 < n
  → Total work: n (inserts) + n (rehash copies) = 2n = O(n)
  → Amortized: O(1) per insert

IMPORTANT NUANCE:
  → The EXPECTED cost of a single insert (without rehash) is O(1)
    due to good hash function (AVERAGE case)
  → The AMORTIZED cost of rehashing is O(1)
    (AMORTIZED analysis)
  → Together: hash table insert is O(1) on average AND amortized

  → But! A single insert CAN take O(n) in the worst case
  → This matters for REAL-TIME systems where every operation 
    must be fast (not just on average)
Example 6 — Splay Trees
text

WHAT IT IS:
  → A self-balancing BST
  → On every access (search, insert, delete), the accessed node
    is "splayed" (moved) to the root using rotations

THE WORRY:
  → A single splay operation can take O(n) (if tree is a long chain)
  → n operations → O(n²)?

AMORTIZED RESULT:
  → Any sequence of m operations on an n-node splay tree
    takes O(m log n) total time
  → Amortized cost per operation = O(log n)
  → Same as balanced BSTs (AVL, Red-Black) — WITHOUT maintaining 
    balance explicitly!

HOW (Physicist's Method):
  → Define potential Φ = Σ log(size of subtree rooted at each node)
  → Splay operation restructures the tree
  → Expensive splay → tree becomes more balanced → potential drops
  → Cheap splay → tree was already balanced → potential stays low
  → The potential function perfectly captures the "debt" of imbalance

WHY THIS IS REMARKABLE:
  → Splay trees are SIMPLER than AVL/Red-Black trees
  → No balance factors, no color bits, no explicit rebalancing rules
  → Just "move accessed node to root"
  → Amortized analysis PROVES this simple strategy is efficient
  → Without amortized analysis, we'd think splay trees are terrible
Example 7 — Queue Using Two Stacks
text

SETUP:
  → Implement a QUEUE using TWO STACKS
  → Stack 1 (inbox): for enqueue operations
  → Stack 2 (outbox): for dequeue operations

OPERATIONS:
  → ENQUEUE: Push to inbox — O(1)
  → DEQUEUE: 
    → If outbox is not empty: pop from outbox — O(1)
    → If outbox IS empty: pour ALL elements from inbox 
      to outbox, then pop — O(n)

THE WORRY:
  → A single DEQUEUE can cost O(n) (pouring everything)
  → n operations → O(n²)?

AMORTIZED ANALYSIS (Banker's Method):
  → Charge 2 for each ENQUEUE:
    → 1 to push to inbox
    → 1 saved as credit (for the future pour to outbox)
  → Charge 0 for each DEQUEUE:
    → The "pouring" is paid by the credits from ENQUEUE
    → The actual pop from outbox is paid by remaining credit

  Each element is:
    → Pushed to inbox once:     paid by ENQUEUE
    → Popped from inbox once:   paid by credit from ENQUEUE
    → Pushed to outbox once:    paid by credit from ENQUEUE
    → Popped from outbox once:  paid by DEQUEUE charge

  Total movements per element = 4 = O(1)
  Credits never go negative ✅

AMORTIZED COST:
  → ENQUEUE: O(1) amortized
  → DEQUEUE: O(1) amortized

THE KEY INSIGHT:
  → Each element passes through the system EXACTLY ONCE
  → It enters inbox, moves to outbox, and leaves
  → Total work per element = constant
  → Total work for n elements = O(n)
  → Even though individual dequeues can be expensive
📊 Amortized Analysis in Common DSA Patterns
text

┌─────────────────────────────────────┬──────────┬───────────┬────────────────┐
│ Data Structure / Pattern            │ Worst    │ Amortized │ Why Amortized  │
│                                     │ Case     │ Cost      │ is Better      │
├─────────────────────────────────────┼──────────┼───────────┼────────────────┤
│ Dynamic Array (push_back)           │ O(n)     │ O(1)      │ Resize is rare │
├─────────────────────────────────────┼──────────┼───────────┼────────────────┤
│ Hash Map (insert with rehash)       │ O(n)     │ O(1)      │ Rehash is rare │
├─────────────────────────────────────┼──────────┼───────────┼────────────────┤
│ Stack Multipop                      │ O(n)     │ O(1)      │ Can't pop more │
│                                     │          │           │ than pushed    │
├─────────────────────────────────────┼──────────┼───────────┼────────────────┤
│ Queue with Two Stacks               │ O(n)     │ O(1)      │ Each element   │
│                                     │          │           │ transferred 1x │
├─────────────────────────────────────┼──────────┼───────────┼────────────────┤
│ Binary Counter Increment            │ O(k)     │ O(1)      │ High bits flip │
│                                     │          │           │ exponentially  │
│                                     │          │           │ less often     │
├─────────────────────────────────────┼──────────┼───────────┼────────────────┤
│ Splay Tree Operations               │ O(n)     │ O(log n)  │ Splaying       │
│                                     │          │           │ balances tree  │
├─────────────────────────────────────┼──────────┼───────────┼────────────────┤
│ Union-Find (with path compression  │ O(n)     │ O(α(n))   │ Path compress  │
│  + union by rank)                   │          │ ≈ O(1)    │ flattens tree  │
├─────────────────────────────────────┼──────────┼───────────┼────────────────┤
│ Fibonacci Heap (decrease key)       │ O(n)     │ O(1)      │ Cascading cuts │
│                                     │          │           │ are rare       │
├─────────────────────────────────────┼──────────┼───────────┼────────────────┤
│ Two Pointer / Sliding Window        │ O(n)     │ O(1) per  │ Each pointer   │
│ (inner loop)                        │ inner    │ outer     │ moves ≤ n      │
│                                     │ iteration│ iteration │ total          │
├─────────────────────────────────────┼──────────┼───────────┼────────────────┤
│ Monotonic Stack (build)             │ O(n)     │ O(1) per  │ Each element   │
│                                     │ per push │ element   │ pushed and     │
│                                     │ (pops)   │           │ popped once    │
├─────────────────────────────────────┼──────────┼───────────┼────────────────┤
│ KMP Pattern Matching                │ O(m) per │ O(1) per  │ Failure func   │
│ (failure function)                  │ mismatch │ character │ bounds total   │
│                                     │          │           │ backtrack      │
├─────────────────────────────────────┼──────────┼───────────┼────────────────┤
│ Move-to-Front (linked list search)  │ O(n)     │ Depends   │ Frequently     │
│                                     │          │ on access │ accessed items │
│                                     │          │ pattern   │ bubble up      │
└─────────────────────────────────────┴──────────┴───────────┴────────────────┘
🔎 How to Recognize Amortized O(1) in Interviews
In interviews, you rarely need to formally PROVE amortized complexity. You need to RECOGNIZE and EXPLAIN it.

The Recognition Signals
text

SIGNAL 1: "Something expensive happens, but it RESETS the state"
  → Resizing resets the array to half-full
  → Pouring stack resets inbox to empty
  → These expensive operations make FUTURE operations cheap
  → CLASSIC AMORTIZED PATTERN

SIGNAL 2: "Each element is processed a constant number of times"
  → Sliding window: each element enters and exits once → 2 times
  → Monotonic stack: each element pushed once and popped once → 2 times
  → Queue with two stacks: each element moves inbox→outbox once
  → If every element is touched O(1) times → total is O(n) → amortized O(1)

SIGNAL 3: "Nested loops, but inner counter doesn't reset"
  → Two pointer: inner pointer only moves forward
  → It's NOT truly nested — it's "interleaved"
  → Total iterations of inner loop across ALL outer iterations = O(n)

SIGNAL 4: "The expensive case can't happen too often"
  → Rehashing: happens at sizes 1, 2, 4, 8, ... → O(log n) times
  → Each time costs more, but happens exponentially less
  → Geometric series → bounded total

SIGNAL 5: "An operation undoes work from previous operations"
  → Multipop undoes pushes
  → Binary counter flips flip back
  → The "undone" work was already paid for when it was "done"
The Counting Argument (Most Common in Interviews)
text

THE UNIVERSAL PROOF TECHNIQUE:

  "Each element enters [the data structure] at most once
   and exits at most once.
   So the total number of enters + exits ≤ 2n.
   Therefore, the total work is O(n),
   and the amortized cost per operation is O(1)."

THIS ARGUMENT WORKS FOR:
  → Sliding window (element enters/exits window once)
  → Monotonic stack (element pushed/popped once)
  → Queue with two stacks (element moves inbox→outbox once)
  → Stack with multipop (element pushed/popped once)
  → BFS/DFS (each node visited once, each edge processed once)

IN AN INTERVIEW, THIS IS USUALLY SUFFICIENT.
You don't need the formal potential function.
🔀 Amortized vs Average — The Critical Difference
text

THIS DISTINCTION COMES UP IN INTERVIEWS.
Get it right.

╔══════════════════════════════════════════════════════════════╗
║                                                              ║
║  AVERAGE CASE:                                               ║
║  → Assumes a PROBABILITY DISTRIBUTION on inputs              ║
║  → "Over random inputs, expected cost is X"                  ║
║  → CAN be wrong if input isn't random                        ║
║  → Example: QuickSort is O(n log n) AVERAGE                  ║
║    but O(n²) worst case (bad pivot every time)               ║
║                                                              ║
║  AMORTIZED:                                                  ║
║  → NO probability assumptions                                ║
║  → "Over ANY sequence of n operations, average cost is X"    ║
║  → GUARANTEED upper bound on total work                      ║
║  → Example: Dynamic array append is O(1) AMORTIZED           ║
║    meaning n appends ALWAYS cost O(n) total                  ║
║                                                              ║
║  KEY DIFFERENCE:                                              ║
║  → Average case: a bad input sequence CAN cause O(n²)        ║
║  → Amortized: even the WORST input sequence is bounded       ║
║                                                              ║
║  AMORTIZED IS A STRONGER GUARANTEE THAN AVERAGE.             ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
The QuickSort vs Dynamic Array Comparison
text

QUICKSORT:
  → Average case: O(n log n) — with random pivot
  → Worst case: O(n²) — sorted input with bad pivot selection
  → This is AVERAGE case, NOT amortized
  → Because specific inputs CAN cause worst case behavior
  → We need probability (randomized pivot) for the guarantee

DYNAMIC ARRAY:
  → Amortized: O(1) per append
  → This means: n appends ALWAYS cost O(n), regardless of input
  → There is NO "bad input" that makes n appends cost O(n²)
  → The guarantee is UNCONDITIONAL

WHY THE CONFUSION:
  → Both say "on average, it's X"
  → But "average" means different things:
    → Average case: average over RANDOM INPUTS
    → Amortized: average over a SEQUENCE OF OPERATIONS (any input)
Another Way to See It
text

AVERAGE CASE says:
  "MOST of the time, a single operation costs O(1)"
  → But sometimes it costs O(n) and you can't predict when
  → No guarantee about total cost of n operations

AMORTIZED says:
  "A single operation MIGHT cost O(n)"
  → But n operations ALWAYS cost O(n) total
  → GUARANTEED: total ÷ n = O(1) per operation
  → The expensive ones are "paid for" by the cheap ones

PRACTICAL DIFFERENCE:
  → For most applications: both are fine
  → For real-time systems: amortized is BETTER than average
    (because it's guaranteed, not probabilistic)
  → For absolute worst-case guarantees on EVERY operation:
    neither is sufficient — you need true O(1) worst case
🚫 Common Misconceptions
Misconception 1: "Amortized O(1) means every operation is O(1)"
text

❌ WRONG

TRUTH:
  → Individual operations CAN be expensive (O(n))
  → But over n operations, the TOTAL is O(n)
  → So the AVERAGE per operation is O(1)
  → Some operations ARE O(n) — but they happen rarely enough

ANALOGY:
  → Your average monthly expense is $1000
  → But in December you spend $5000 (holidays)
  → And in June you spend $200
  → Average is still ~$1000/month
  → That doesn't mean every month costs exactly $1000
Misconception 2: "Amortized analysis uses probability"
text

❌ WRONG

TRUTH:
  → Amortized analysis is 100% DETERMINISTIC
  → No randomness, no probability, no expected values
  → It's about the STRUCTURE of the operations, not random inputs
  → The "average" in amortized is over a SEQUENCE, not over random trials

  COMPARISON:
    → Average case of QuickSort: uses probability (random pivot)
    → Amortized cost of dynamic array: NO probability (it's ALWAYS O(1))
Misconception 3: "If amortized is O(1), then n operations cost exactly O(n)"
text

⚠️ MOSTLY RIGHT, but be precise

TRUTH:
  → n operations cost AT MOST O(n) (upper bound)
  → They could cost LESS (e.g., if no resize ever triggers)
  → Amortized is an UPPER BOUND on the average, not the exact average
  → Formally: Total cost ≤ c × n for some constant c
Misconception 4: "Amortized analysis makes worst case irrelevant"
text

❌ WRONG

TRUTH:
  → Amortized analysis tells you about the TOTAL cost of n operations
  → But a SINGLE operation can still be O(n)
  → In real-time systems (pacemaker, autopilot), a single O(n) 
    operation could be catastrophic
  → For latency-sensitive applications, you might need 
    TRUE O(1) worst case, not just amortized O(1)

  EXAMPLE:
    → Dynamic array append: amortized O(1), worst case O(n)
    → If you NEED every append to be O(1): 
      use a different data structure
      (e.g., linked list: true O(1) append, but O(n) access)
Misconception 5: "Only fancy data structures need amortized analysis"
text

❌ WRONG

TRUTH:
  → Amortized analysis appears in the simplest DSA patterns:
    → Sliding window → amortized O(1) per element
    → Monotonic stack → amortized O(1) per element
    → Two pointers → amortized O(1) per step
    → Even simple Python list.append() → amortized O(1)

  → You're ALREADY using amortized analysis every day
  → You just might not realize it
Misconception 6: "Amortized O(1) is worse than worst-case O(1)"
text

✅ TECHNICALLY TRUE — but context matters

COMPARISON:
  → Worst-case O(1): EVERY operation is O(1), guaranteed
  → Amortized O(1): n operations total O(n), individual can be O(n)

  → Worst-case O(1) is STRICTLY STRONGER
  → But amortized O(1) is strong enough for 99% of applications
  → And data structures with amortized O(1) are often SIMPLER 
    and FASTER in practice (lower constant factors)

EXAMPLE:
  → Dynamic array (amortized O(1) append): simple, cache-friendly, fast
  → Linked list (worst-case O(1) append): pointer overhead, cache-unfriendly
  → In practice, dynamic array is almost always FASTER
💼 Interview Questions Involving Amortized Analysis
Questions Where You Need to Explain Amortized Cost
text

QUESTION 1: "What's the time complexity of n push_back operations 
              on a vector/ArrayList?"
  
  WRONG ANSWER: "O(n²) because a single push_back can be O(n)"
  
  RIGHT ANSWER: "O(n) total, which is O(1) amortized per operation.
                 While a single push_back CAN be O(n) during resizing,
                 resizing happens at sizes 1, 2, 4, 8, ..., and the 
                 total cost of all resizes is a geometric series
                 that sums to O(n). So each push_back is O(1) amortized."


QUESTION 2: "What's the time complexity of your sliding window solution?"

  WRONG ANSWER: "O(n²) because the inner while loop can run n times"
  
  RIGHT ANSWER: "O(n). While the inner loop can run up to n times
                 for a SINGLE iteration of the outer loop, the left
                 pointer only moves right and never resets. Over ALL
                 iterations of the outer loop, the inner loop runs
                 at most n times total. So it's O(n) total, or
                 amortized O(1) per element."


QUESTION 3: "Implement a queue using two stacks. What's the complexity?"

  WRONG ANSWER: "Dequeue is O(n) because we might need to transfer 
                 all elements"
  
  RIGHT ANSWER: "Amortized O(1) for both enqueue and dequeue.
                 Each element is pushed to the inbox once, transferred
                 to the outbox once, and popped from the outbox once.
                 That's O(1) work per element across its entire lifetime.
                 So n operations cost O(n) total."


QUESTION 4: "Why is Union-Find nearly O(1) per operation?"

  RIGHT ANSWER: "With both path compression and union by rank,
                 each Find operation is O(α(n)) amortized, where
                 α is the inverse Ackermann function. α(n) ≤ 4
                 for any practical n (up to 10^80), so it's
                 effectively O(1) per operation."


QUESTION 5: "What's the complexity of building a monotonic stack 
              from an array of n elements?"

  WRONG ANSWER: "O(n²) because for each element, we might pop 
                 many elements"
  
  RIGHT ANSWER: "O(n). Each of the n elements is pushed onto the
                 stack exactly once and popped at most once. Total
                 push + pop operations ≤ 2n = O(n). So the amortized
                 cost per element is O(1)."
Follow-Up Questions You Might Get
text

Q: "But what if I need EVERY operation to be O(1), not just amortized?"
A: "Then a dynamic array isn't suitable. You'd need a linked list
    for O(1) worst-case append, or a balanced BST for O(log n) 
    worst-case everything. But you sacrifice cache locality and 
    practical speed."

Q: "Is amortized the same as average case?"
A: "No. Average case assumes random inputs and uses probability.
    Amortized gives a guaranteed bound over ANY sequence of 
    operations — no randomness involved. Amortized is a 
    stronger guarantee."

Q: "When would amortized O(1) NOT be acceptable?"
A: "In hard real-time systems where every operation must complete
    within a strict time bound — like embedded systems, trading 
    engines, or safety-critical software. A single O(n) spike
    could violate the timing constraint."

Q: "Can an algorithm have amortized complexity worse than worst case?"
A: "No. Amortized cost is always ≤ worst-case cost per operation.
    Amortized provides a TIGHTER (better) bound."
🎙️ How to Explain Amortized Analysis in an Interview
The 30-Second Explanation
text

"Amortized O(1) means that while a single operation might 
occasionally be expensive — like O(n) during a resize — 
this happens so rarely that when you average the cost over 
n operations, each one is effectively O(1).

The key insight is that an expensive operation like resizing 
can only happen AFTER many cheap operations. The cheap operations 
'pay forward' for the expensive one. So the total cost of 
n operations is O(n), giving O(1) per operation amortized."
The 10-Second Explanation (When Pressed for Time)
text

"Each element is processed a constant number of times total.
 n elements × O(1) work each = O(n) total = O(1) amortized."
For Sliding Window Specifically
text

"The left pointer and right pointer each move at most n times 
total across the entire algorithm. So even though there's an 
inner loop, the total work is O(n) + O(n) = O(n). Each element 
is visited at most twice — once by each pointer."
For Dynamic Array Specifically
text

"When the array doubles from size n to 2n, it copies n elements — 
that's expensive. But it won't need to copy again until n MORE 
inserts happen. So you do n cheap inserts, then 1 expensive one. 
The expensive one is 'paid for' by the n cheap ones. Total cost 
of 2n inserts = n (copies) + 2n (inserts) = O(n). Amortized O(1)."
📝 Practice Problems
Problems Where Understanding Amortized Analysis Helps
text

TIER 1 — RECOGNIZE AMORTIZED O(1) IN YOUR OWN SOLUTIONS

  □ Two Sum (Hash Map: O(1) amortized lookup with rehashing)
  □ Longest Substring Without Repeating Characters (Sliding Window)
  □ Minimum Window Substring (Sliding Window)
  □ Next Greater Element (Monotonic Stack)
  □ Daily Temperatures (Monotonic Stack)
  □ Trapping Rain Water (Two Pointers variant)
  □ Subarray Sum Equals K (Prefix Sum with Hash Map)
  □ Sliding Window Maximum (Monotonic Deque)

TIER 2 — PROBLEMS WHERE AMORTIZED IS THE KEY INSIGHT

  □ Implement Queue using Stacks (LC #232)
  □ Implement Stack using Queues (LC #225)
  □ Min Stack (LC #155)
  □ Online Stock Span (LC #901) — Monotonic Stack
  □ Number of Visible People in a Queue (LC #1944) — Monotonic Stack
  □ Shortest Subarray with Sum at Least K (LC #862) — Monotonic Deque

TIER 3 — PROBLEMS WHERE AMORTIZED IS HIDDEN

  □ Redundant Connection (LC #684) — Union Find
  □ Accounts Merge (LC #721) — Union Find
  □ Number of Provinces (LC #547) — Union Find
  □ Design HashMap (LC #706) — Rehashing
  □ LRU Cache (LC #146) — Amortized O(1) get/put

TIER 4 — ADVANCED (COMPETITIVE PROGRAMMING)

  □ Splay tree problems
  □ Link-Cut Tree problems
  □ Fibonacci heap applications
  □ Heavy-light decomposition with amortized updates
Self-Test Questions
text

TEST YOURSELF — Can you explain:

  1. Why is dynamic array append O(1) amortized, not O(n)?
  2. Why is sliding window O(n) total, not O(n²)?
  3. Why is monotonic stack construction O(n)?
  4. What's the difference between amortized and average case?
  5. When is amortized O(1) NOT good enough?
  6. How does the Banker's Method work? (conceptually)
  7. Why does the growth factor need to be multiplicative 
     (×2), not additive (+k)?
  8. Why is Union-Find effectively O(1) per operation?
  9. How would you explain amortized analysis to a 
     non-technical person?
  10. Can you give an example where worst-case analysis 
      is misleadingly pessimistic?
📇 Quick Reference Card
text

╔══════════════════════════════════════════════════════════════════╗
║              AMORTIZED ANALYSIS — QUICK REFERENCE               ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║  WHAT IT IS:                                                     ║
║    Average cost per operation over a worst-case sequence         ║
║    of n operations. NO probability assumptions.                  ║
║                                                                  ║
║  WHEN TO USE:                                                    ║
║    When worst case per operation is high but happens rarely.     ║
║    When expensive ops "reset" the state, making future ops       ║
║    cheap.                                                        ║
║                                                                  ║
║  THREE METHODS:                                                  ║
║    1. AGGREGATE: Total cost T(n) / n = amortized cost           ║
║    2. BANKER'S: Overcharge cheap ops, save credit for            ║
║       expensive ops. Credit ≥ 0 always.                         ║
║    3. PHYSICIST'S: ĉᵢ = cᵢ + Φ(Dᵢ) - Φ(Dᵢ₋₁)                ║
║       Define Φ so that Φ(final) ≥ Φ(initial).                  ║
║                                                                  ║
║  COMMON EXAMPLES:                                                ║
║    → Dynamic array append:     O(1) amortized                   ║
║    → Hash table insert:        O(1) amortized                   ║
║    → Stack multipop:           O(1) amortized                   ║
║    → Queue with two stacks:    O(1) amortized                   ║
║    → Binary counter increment: O(1) amortized                   ║
║    → Sliding window:           O(1) amortized per element       ║
║    → Monotonic stack:          O(1) amortized per element       ║
║    → Splay tree:               O(log n) amortized               ║
║    → Union-Find (optimized):   O(α(n)) ≈ O(1) amortized        ║
║                                                                  ║
║  KEY INSIGHT:                                                    ║
║    "Each element is processed O(1) times across all operations   ║
║     → total work O(n) → amortized O(1)"                        ║
║                                                                  ║
║  AMORTIZED ≠ AVERAGE CASE:                                      ║
║    → Average: probability-based, input-dependent                ║
║    → Amortized: guaranteed, worst-case sequence                 ║
║    → Amortized is a STRONGER guarantee                          ║
║                                                                  ║
║  IN INTERVIEWS:                                                  ║
║    → Use the "counting argument" (each element O(1) work)       ║
║    → Don't need formal proofs — just clear reasoning            ║
║    → Know the dynamic array and sliding window explanations      ║
║    → Know the difference from average case                       ║
║                                                                  ║
╚══════════════════════════════════════════════════════════════════╝
⭐ Star this repo if amortized analysis finally clicked for you. Share it with someone who's confused by "O(1) amortized."

