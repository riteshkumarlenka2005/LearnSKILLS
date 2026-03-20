📊 Tracking Progress — The Complete Problem Log System
What gets measured gets managed. What gets tracked gets mastered. Without a system to track your DSA journey, you're walking blind.

📌 Table of Contents
Why Tracking Matters
The 3 Pillars of Progress Tracking
The Problem Log Template
How to Fill the Problem Log
The Daily Log
The Weekly Review Template
The Monthly Review Template
The Revision System — Spaced Repetition
The Weakness Tracker
The Pattern Mastery Matrix
The Confidence Meter
The Mistake Journal
The Key Insight Notebook
Contest & Mock Interview Tracker
Tools & Where to Maintain Your Log
Sample Filled Log — 2 Weeks Example
The Anti-Patterns — Tracking Mistakes to Avoid
Printable Checklists
💡 Why Tracking Matters
text

WITHOUT TRACKING:
  → "I've been practicing for 3 months" (but no idea how many problems)
  → "I feel like I'm not improving" (but no data to confirm or deny)
  → "I keep forgetting problems" (but no revision schedule)
  → "I don't know what I'm weak at" (but haven't analyzed patterns)
  → "I'll just do random problems" (but no direction or structure)

WITH TRACKING:
  → "I've solved 187 problems — 52 easy, 108 medium, 27 hard"
  → "My sliding window accuracy went from 40% to 85% in 6 weeks"
  → "I have 12 problems due for revision this week"
  → "I struggle most with DP on trees and binary search on answer"
  → "At this pace, I'll hit my target of 300 problems by interview date"
The Science Behind It
text

TRACKING WORKS BECAUSE OF:

1. THE HAWTHORNE EFFECT
   → You perform better when you KNOW you're being measured
   → Even self-measurement creates accountability

2. FEEDBACK LOOPS
   → Data shows you what's working and what isn't
   → You can adjust your strategy based on EVIDENCE, not feelings

3. MOTIVATION THROUGH PROGRESS
   → Seeing "143 problems solved" feels incredible
   → Progress bars are psychologically powerful
   → Small wins compound into massive confidence

4. IDENTIFYING BLIND SPOTS
   → "I've solved 40 array problems but only 3 graph problems"
   → Without data, you won't notice these gaps

5. SPACED REPETITION
   → Tracking WHEN you solved something enables WHEN to revisit
   → This is the #1 hack for long-term retention
🏛️ The 3 Pillars of Progress Tracking
text

PILLAR 1 — THE PROBLEM LOG
  → Every problem you attempt, documented
  → The CORE of your tracking system
  → Records what you solved, how you solved it, and what you learned

PILLAR 2 — THE REVIEW SYSTEM
  → Daily, weekly, and monthly check-ins
  → Scheduled revision of past problems
  → Pattern and weakness analysis

PILLAR 3 — THE INSIGHT JOURNAL
  → Key learnings, "aha" moments, and mistakes
  → Patterns you've discovered
  → Your personal cheat sheets that evolve over time
📋 The Problem Log Template
This is the heart of your tracking system. One row per problem. Fill it EVERY TIME.

The Core Columns
text

┌──────────────────────────────────────────────────────────────────────────────┐
│                        PROBLEM LOG — CORE TEMPLATE                          │
├────┬───────────┬──────────┬────────┬──────┬────────┬────────┬──────────────┤
│ #  │ Date      │ Problem  │Platform│ Diff │ Topic/ │ Status │ Time Taken   │
│    │           │ Name     │        │      │ Pattern│        │              │
├────┼───────────┼──────────┼────────┼──────┼────────┼────────┼──────────────┤
│ 1  │2024-01-15 │ Two Sum  │LeetCode│ Easy │Hashing │  ✅    │ 12 min       │
├────┼───────────┼──────────┼────────┼──────┼────────┼────────┼──────────────┤
│ 2  │2024-01-15 │ 3Sum     │LeetCode│ Med  │Two Ptr │  🔶   │ 45 min       │
├────┼───────────┼──────────┼────────┼──────┼────────┼────────┼──────────────┤
│ 3  │2024-01-16 │ LCA of   │LeetCode│ Med  │Tree/DFS│  ❌   │ 50 min       │
│    │           │ BST      │        │      │        │        │ (gave up)    │
└────┴───────────┴──────────┴────────┴──────┴────────┴────────┴──────────────┘

STATUS LEGEND:
  ✅ — Solved independently (no hints, no looking up)
  🔶 — Solved with hints (needed 1-2 nudges or looked at approach)
  ❌ — Could not solve (looked at full solution)
  🔁 — Revision attempt (re-solving a past problem)
The Extended Columns
text

┌────────────────────────────────────────────────────────────────────────────────────┐
│                    PROBLEM LOG — EXTENDED TEMPLATE                                  │
├────────┬────────────┬───────────┬──────────┬──────────┬──────────┬─────────────────┤
│Approach│ Time       │ Space     │ Key      │ Mistakes │ Revisit  │ Revision        │
│ Used   │ Complexity │ Complexity│ Insight  │ Made     │ Date     │ Status          │
├────────┼────────────┼───────────┼──────────┼──────────┼──────────┼─────────────────┤
│HashMap │ O(n)       │ O(n)      │Complement│ None     │2024-01-18│ ✅ Easy on rev  │
│lookup  │            │           │in map    │          │          │                 │
├────────┼────────────┼───────────┼──────────┼──────────┼──────────┼─────────────────┤
│Sort +  │ O(n²)      │ O(1)      │Skip dupes│Off-by-one│2024-01-19│ 🔶 Forgot skip  │
│2 ptrs  │            │           │in sorted │in inner  │          │   duplicates    │
├────────┼────────────┼───────────┼──────────┼──────────┼──────────┼─────────────────┤
│Recursive│ O(n)      │ O(h)      │BST prop: │Didn't use│2024-01-19│ ✅ Got it!      │
│DFS     │            │           │left<root │BST prop  │          │                 │
│        │            │           │<right    │at first  │          │                 │
└────────┴────────────┴───────────┴──────────┴──────────┴──────────┴─────────────────┘
The Complete Column Reference
Column	What to Record	Why It Matters
#	Sequential number	Track total count easily
Date	When you attempted it	Enables spaced repetition scheduling
Problem Name	Full name + link if possible	Easy to find again for revision
Platform	LeetCode / GFG / Codeforces / etc.	Know where to revisit
Difficulty	Easy / Medium / Hard	Track difficulty distribution
Topic / Pattern	Primary technique used	Identify strong and weak patterns
Status	✅ / 🔶 / ❌ / 🔁	Honest self-assessment
Time Taken	Actual minutes spent	Track speed improvement over time
Approach Used	Brief description of method	Recall your thought process
Time Complexity	Big O of your solution	Practice complexity analysis
Space Complexity	Big O of space used	Practice complexity analysis
Key Insight	The "aha" moment	THE most valuable column for learning
Mistakes Made	What went wrong	Prevent repeating the same errors
Revisit Date	When to re-attempt	Spaced repetition scheduling
Revision Status	How revision went	Track long-term retention
✍️ How to Fill the Problem Log
The 2-Minute Post-Solve Ritual
text

IMMEDIATELY after solving (or failing to solve) every problem:

STEP 1 (30 sec): Record the basics
  → Date, problem name, platform, difficulty, topic

STEP 2 (30 sec): Record the honest status
  → ✅ ​🔶 or ❌ — NO LYING TO YOURSELF
  → Record actual time taken (be honest)

STEP 3 (30 sec): Record the approach
  → What technique did you use?
  → Time and space complexity

STEP 4 (30 sec): Record the LEARNING
  → What was the key insight?
  → What mistake did you make?
  → THIS IS THE MOST IMPORTANT PART

STEP 5 (Set the revisit date)
  → ✅ problems: revisit in 7 days
  → 🔶 problems: revisit in 3 days
  → ❌ problems: revisit in 1 day, then 3 days, then 7 days
What to Write in "Key Insight"
text

BAD INSIGHTS (too vague):
  ❌ "Use DP"
  ❌ "Hash map helps"
  ❌ "It was tricky"

GOOD INSIGHTS (specific and reusable):
  ✅ "The complement (target - current) can be looked up in O(1) using a hash map"
  ✅ "In a sorted array, duplicates must be skipped AFTER finding a valid pair, 
      not before checking"
  ✅ "For BST problems, the key property is: everything in left subtree < root 
      < everything in right subtree — USE this to prune recursion"
  ✅ "When the problem says 'contiguous subarray with condition X', 
      think SLIDING WINDOW first"
  ✅ "Binary search works here because the answer space is monotonic: 
      if X works, X+1 also works"
What to Write in "Mistakes Made"
text

BAD MISTAKE ENTRIES:
  ❌ "Made a mistake"
  ❌ "Got it wrong"
  ❌ "Took too long"

GOOD MISTAKE ENTRIES:
  ✅ "Used < instead of <= in the binary search condition, causing off-by-one"
  ✅ "Forgot to handle the case where the array is empty"
  ✅ "Started with brute force but didn't optimize — 
      should have recognized the sliding window pattern earlier"
  ✅ "Tried to use DFS when BFS was needed 
      (problem asked for SHORTEST path = BFS)"
  ✅ "Forgot that Python heapq is min-heap — 
      negated values for max-heap but forgot to negate back on pop"
  ✅ "Spent 20 minutes coding before planning — 
      had to rewrite from scratch"
📅 The Daily Log
A quick snapshot of each day's practice. Takes 2 minutes to fill.

text

╔══════════════════════════════════════════════════════════════╗
║                    DAILY LOG TEMPLATE                        ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  Date: _______________                                       ║
║                                                              ║
║  Problems Attempted:  ___                                    ║
║  Problems Solved (✅): ___                                   ║
║  Problems with Hints (🔶): ___                               ║
║  Problems Failed (❌): ___                                   ║
║  Revisions Done (🔁): ___                                    ║
║                                                              ║
║  Total Time Spent: ___ hours ___ minutes                     ║
║                                                              ║
║  Topics Covered Today:                                       ║
║    □ ___________________                                     ║
║    □ ___________________                                     ║
║                                                              ║
║  Best Moment Today:                                          ║
║    ________________________________________________          ║
║    (something you solved well or an insight you gained)      ║
║                                                              ║
║  Struggle Point Today:                                       ║
║    ________________________________________________          ║
║    (what was hardest and why)                                ║
║                                                              ║
║  Tomorrow's Plan:                                            ║
║    ________________________________________________          ║
║    (what topics/problems will you focus on)                  ║
║                                                              ║
║  Mood/Energy: 😤 😐 🙂 😊 🔥                               ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
Why Track Mood/Energy?
text

PATTERNS YOU'LL DISCOVER:

  → "I solve better in the morning — schedule hard problems then"
  → "After 2 hours, my accuracy drops — take breaks"
  → "I'm frustrated because I did 5 DP problems in a row — mix topics"
  → "My energy is high on weekends — do contests then"
  → "I'm burning out — need a rest day"

THIS DATA PREVENTS BURNOUT.
You can't manage what you don't measure.
📆 The Weekly Review Template
Every Sunday (or your chosen day), spend 30-45 minutes on this review.

text

╔══════════════════════════════════════════════════════════════╗
║                  WEEKLY REVIEW TEMPLATE                      ║
║                  Week of: _______________                    ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  ── NUMBERS ──                                               ║
║                                                              ║
║  Total Problems Attempted:    ___                            ║
║  Solved Independently (✅):   ___ ( __% )                   ║
║  Solved with Hints (🔶):      ___ ( __% )                   ║
║  Could Not Solve (❌):        ___ ( __% )                   ║
║  Revisions Completed (🔁):    ___                            ║
║  Total Time Spent:            ___ hours                      ║
║  Average Time per Problem:    ___ minutes                    ║
║                                                              ║
║  ── DIFFICULTY BREAKDOWN ──                                  ║
║                                                              ║
║  Easy:    ___ attempted / ___ solved                         ║
║  Medium:  ___ attempted / ___ solved                         ║
║  Hard:    ___ attempted / ___ solved                         ║
║                                                              ║
║  ── TOPIC BREAKDOWN ──                                       ║
║                                                              ║
║  Arrays:           ___ problems                              ║
║  Strings:          ___ problems                              ║
║  Hashing:          ___ problems                              ║
║  Two Pointers:     ___ problems                              ║
║  Sliding Window:   ___ problems                              ║
║  Binary Search:    ___ problems                              ║
║  Stacks/Queues:    ___ problems                              ║
║  Trees:            ___ problems                              ║
║  Graphs:           ___ problems                              ║
║  DP:               ___ problems                              ║
║  Greedy:           ___ problems                              ║
║  Backtracking:     ___ problems                              ║
║  Other:            ___ problems                              ║
║                                                              ║
║  ── REFLECTION ──                                            ║
║                                                              ║
║  What went WELL this week?                                   ║
║  ___________________________________________________         ║
║  ___________________________________________________         ║
║                                                              ║
║  What DIDN'T go well?                                        ║
║  ___________________________________________________         ║
║  ___________________________________________________         ║
║                                                              ║
║  What PATTERNS am I getting better at?                       ║
║  ___________________________________________________         ║
║                                                              ║
║  What PATTERNS am I still struggling with?                   ║
║  ___________________________________________________         ║
║                                                              ║
║  What MISTAKES did I repeat this week?                       ║
║  ___________________________________________________         ║
║                                                              ║
║  ── PLAN FOR NEXT WEEK ──                                    ║
║                                                              ║
║  Focus Topics:                                               ║
║    1. ___________________                                    ║
║    2. ___________________                                    ║
║                                                              ║
║  Target Problem Count: ___                                   ║
║                                                              ║
║  Revisions Due: ___ problems                                 ║
║                                                              ║
║  Specific Goals:                                             ║
║    □ ___________________                                     ║
║    □ ___________________                                     ║
║    □ ___________________                                     ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
The Key Metrics to Watch Weekly
text

METRIC 1: SOLVE RATE
  → (✅ + 🔶) / Total Attempted
  → Target: 70%+ (if below, problems are too hard or you need more foundation)
  → If above 90%: increase difficulty

METRIC 2: INDEPENDENCE RATE
  → ✅ / (✅ + 🔶 + ❌)
  → Target: 50%+ and INCREASING week over week
  → This is the truest measure of growth

METRIC 3: AVERAGE TIME
  → Total time / Problems solved
  → Should DECREASE over time for same difficulty level
  → Easy: target <15 min, Medium: target <30 min

METRIC 4: TOPIC COVERAGE
  → Are you avoiding any topics?
  → Are you over-indexing on comfortable topics?
  → Force yourself to practice weak areas

METRIC 5: REVISION COMPLETION
  → Revisions Due / Revisions Completed
  → Target: 100% — never skip revisions
  → Incomplete revisions = future forgotten problems
📊 The Monthly Review Template
Once a month, zoom out and look at the big picture. This takes 1 hour.

text

╔══════════════════════════════════════════════════════════════╗
║                 MONTHLY REVIEW TEMPLATE                      ║
║                 Month: _______________                       ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  ── CUMULATIVE STATS ──                                      ║
║                                                              ║
║  Total Problems Solved (All Time):    ___                    ║
║  Problems Solved This Month:          ___                    ║
║  Total Study Hours This Month:        ___                    ║
║  Contests Participated:               ___                    ║
║  Mock Interviews Done:                ___                    ║
║                                                              ║
║  ── PROGRESS COMPARISON ──                                   ║
║                                                              ║
║             This Month    Last Month    Change               ║
║  Solve Rate:   ___%         ___%        ↑↓ ___%             ║
║  Indep Rate:   ___%         ___%        ↑↓ ___%             ║
║  Avg Time:     ___ min      ___ min     ↑↓ ___ min          ║
║  Problems:     ___          ___         ↑↓ ___              ║
║                                                              ║
║  ── PATTERN MASTERY ASSESSMENT ──                            ║
║                                                              ║
║  Rate yourself 1-5 on each:                                  ║
║                                                              ║
║  Arrays/Strings:    ☆☆☆☆☆  (was ___ last month)            ║
║  Hashing:           ☆☆☆☆☆  (was ___ last month)            ║
║  Two Pointers:      ☆☆☆☆☆  (was ___ last month)            ║
║  Sliding Window:    ☆☆☆☆☆  (was ___ last month)            ║
║  Binary Search:     ☆☆☆☆☆  (was ___ last month)            ║
║  Stacks/Queues:     ☆☆☆☆☆  (was ___ last month)            ║
║  Linked Lists:      ☆☆☆☆☆  (was ___ last month)            ║
║  Trees:             ☆☆☆☆☆  (was ___ last month)            ║
║  Heaps:             ☆☆☆☆☆  (was ___ last month)            ║
║  Graphs:            ☆☆☆☆☆  (was ___ last month)            ║
║  DP:                ☆☆☆☆☆  (was ___ last month)            ║
║  Greedy:            ☆☆☆☆☆  (was ___ last month)            ║
║  Backtracking:      ☆☆☆☆☆  (was ___ last month)            ║
║  Bit Manipulation:  ☆☆☆☆☆  (was ___ last month)            ║
║  Tries:             ☆☆☆☆☆  (was ___ last month)            ║
║                                                              ║
║  ── BIGGEST WINS THIS MONTH ──                               ║
║                                                              ║
║  1. ___________________________________________________      ║
║  2. ___________________________________________________      ║
║  3. ___________________________________________________      ║
║                                                              ║
║  ── BIGGEST CHALLENGES THIS MONTH ──                         ║
║                                                              ║
║  1. ___________________________________________________      ║
║  2. ___________________________________________________      ║
║  3. ___________________________________________________      ║
║                                                              ║
║  ── RECURRING MISTAKES ──                                    ║
║  (patterns you keep making across multiple problems)         ║
║                                                              ║
║  1. ___________________________________________________      ║
║  2. ___________________________________________________      ║
║  3. ___________________________________________________      ║
║                                                              ║
║  ── NEXT MONTH'S STRATEGY ──                                 ║
║                                                              ║
║  Focus Areas:                                                ║
║    1. ___________________                                    ║
║    2. ___________________                                    ║
║                                                              ║
║  Target Problems: ___                                        ║
║  Target Contests: ___                                        ║
║  Target Mocks:    ___                                        ║
║                                                              ║
║  Specific Goals:                                             ║
║    □ ___________________                                     ║
║    □ ___________________                                     ║
║    □ ___________________                                     ║
║                                                              ║
║  ── LONG-TERM PROGRESS ──                                    ║
║                                                              ║
║  Am I on track for my interview/goal date?  YES / NO         ║
║  Do I need to adjust my daily time?         YES / NO         ║
║  Do I need to change my approach?           YES / NO         ║
║                                                              ║
║  Notes: ________________________________________________     ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
The Monthly Star Rating Guide
text

WHAT EACH STAR MEANS:

☆☆☆☆☆  (1/5) — UNFAMILIAR
  → Haven't studied this topic yet
  → Can't recognize when to apply it
  → Need to start from scratch

★☆☆☆☆  (2/5) — AWARE
  → Know the concept exists
  → Can follow a solution but can't derive one
  → Solved fewer than 5 problems

★★☆☆☆  (3/5) — LEARNING
  → Can solve EASY problems in this pattern
  → Need hints for MEDIUM problems
  → Solved 5-15 problems

★★★☆☆  (4/5) — COMFORTABLE
  → Can solve most MEDIUM problems independently
  → Can attempt HARD problems with some hints
  → Solved 15-30 problems
  → Can recognize the pattern in new problems

★★★★☆  (4/5) — STRONG
  → Can solve MEDIUM problems quickly
  → Can solve many HARD problems
  → Can explain the technique to others
  → Rarely need hints

★★★★★  (5/5) — MASTERED
  → Instant pattern recognition
  → Can solve HARD problems and variations
  → Can combine this with other patterns
  → Can teach this topic comprehensively
🔁 The Revision System — Spaced Repetition
Solving a problem once teaches you for a day. Revising it at the right intervals teaches you forever.

The Spaced Repetition Schedule
text

THE SCIENCE:
  → You forget 70% of what you learn within 24 hours (Ebbinghaus curve)
  → Each review STRENGTHENS the memory
  → The gap between reviews can INCREASE each time
  → This is mathematically the most efficient way to remember

THE SCHEDULE:

  Day 0:  Solve the problem for the first time
  Day 1:  First revision (especially for ❌ and 🔶 problems)
  Day 3:  Second revision
  Day 7:  Third revision
  Day 14: Fourth revision
  Day 30: Fifth revision (if you nail this, it's in long-term memory)
How to Track Revisions
text

┌─────────────────────────────────────────────────────────────────┐
│                    REVISION TRACKER                              │
├────┬──────────────┬──────────┬───────┬───────┬──────┬──────────┤
│ #  │ Problem Name │ Solved   │ Rev 1 │ Rev 2 │Rev 3 │ Rev 4    │
│    │              │ Date     │ (+1d) │ (+3d) │(+7d) │ (+14d)   │
├────┼──────────────┼──────────┼───────┼───────┼──────┼──────────┤
│ 1  │ Two Sum      │ Jan 15   │Jan 16 │Jan 18 │Jan 22│ Jan 29   │
│    │              │ ❌       │ 🔶    │ ✅    │ ✅   │ ✅ DONE  │
├────┼──────────────┼──────────┼───────┼───────┼──────┼──────────┤
│ 2  │ 3Sum         │ Jan 15   │Jan 16 │Jan 18 │Jan 22│ Jan 29   │
│    │              │ 🔶       │ 🔶    │ ✅    │ 🔶   │ REDO +7d │
├────┼──────────────┼──────────┼───────┼───────┼──────┼──────────┤
│ 3  │ LCA of BST   │ Jan 16   │Jan 17 │Jan 19 │Jan 23│ Jan 30   │
│    │              │ ❌       │ ❌    │ 🔶    │ ✅   │ ✅ DONE  │
└────┴──────────────┴──────────┴───────┴───────┴──────┴──────────┘

REVISION RULES:
  ✅ on revision → Move to next scheduled revision
  🔶 on revision → Keep the same interval, don't advance
  ❌ on revision → RESET — go back to +1 day interval

DONE = Passed 3 consecutive ✅ revisions → moved to long-term memory
The Revision Session Protocol
text

WHEN REVISING A PROBLEM:

  1. DO NOT look at your old solution
  2. DO NOT look at the problem hints
  3. Read ONLY the problem statement
  4. Try to solve it from scratch
  5. Time yourself (should be FASTER than first attempt)
  6. After solving (or failing), COMPARE with your old solution
  7. Note what you remembered and what you forgot
  8. Update revision status

IMPORTANT:
  → If you can solve it in <5 minutes from memory → 
    you've likely MEMORIZED it, not UNDERSTOOD it
  → The goal is to RE-DERIVE the approach, not recall the code
  → Ask yourself: "WHY does this approach work?"
Daily Revision Queue
text

EACH DAY, before solving NEW problems:

  1. Check your revision tracker for DUE revisions
  2. Do ALL due revisions FIRST (usually 2-5 problems)
  3. This takes 15-30 minutes
  4. THEN move to new problems

WHY REVISIONS FIRST:
  → Protecting existing knowledge > acquiring new knowledge
  → It's like watering plants you've already planted 
    before planting new ones
  → Skipping revisions means those problems were wasted effort
🔍 The Weakness Tracker
Your weaknesses are your biggest opportunities. Track them systematically.

text

╔══════════════════════════════════════════════════════════════╗
║                    WEAKNESS TRACKER                          ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  TOPIC WEAKNESS LOG                                          ║
║                                                              ║
║  ┌──────────────┬────────┬────────┬────────┬──────────────┐  ║
║  │ Topic        │Attempt │ Solved │ Solve  │ Action Plan  │  ║
║  │              │Count   │ Count  │ Rate   │              │  ║
║  ├──────────────┼────────┼────────┼────────┼──────────────┤  ║
║  │ DP           │ 15     │ 6      │ 40%    │ Study theory │  ║
║  │              │        │        │  🔴    │ + 5 easy DPs │  ║
║  ├──────────────┼────────┼────────┼────────┼──────────────┤  ║
║  │ Graphs       │ 8      │ 4      │ 50%    │ Practice BFS │  ║
║  │              │        │        │  🟡    │ & DFS basics │  ║
║  ├──────────────┼────────┼────────┼────────┼──────────────┤  ║
║  │ Sliding Win  │ 10     │ 9      │ 90%    │ Move to hard │  ║
║  │              │        │        │  🟢    │ variations   │  ║
║  └──────────────┴────────┴────────┴────────┴──────────────┘  ║
║                                                              ║
║  SOLVE RATE LEGEND:                                          ║
║    🟢 80-100% — Strong (maintain with occasional practice)   ║
║    🟡 50-79%  — Developing (needs focused practice)          ║
║    🔴 0-49%   — Weak (needs dedicated study + easy problems) ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
The Weakness Analysis Process
text

EVERY 2 WEEKS, do this analysis:

STEP 1: COUNT problems by topic
  → How many attempted? How many solved?

STEP 2: CALCULATE solve rate per topic
  → Solve rate = (✅ + 🔶) / Total attempted × 100

STEP 3: RANK topics from weakest to strongest

STEP 4: CREATE an action plan for the bottom 3 topics
  → If solve rate < 30%: Go back to THEORY. Watch a video. Read notes.
  → If solve rate 30-60%: Solve 5-8 EASY problems in that topic.
  → If solve rate 60-80%: Solve 5-8 MEDIUM problems. Focus on variations.

STEP 5: ADJUST your practice schedule
  → Spend 60% of time on weak topics
  → Spend 40% of time on maintaining strong topics + new learning
The Skill Gap Map
text

A visual way to see where you stand:

                     BEGINNER    LEARNING    COMPETENT   STRONG    MASTER
                     |           |           |           |         |
Arrays               ████████████████████████████████████████████████ ★★★★★
Strings              █████████████████████████████████████████       ★★★★
Hashing              ████████████████████████████████████████████████ ★★★★★
Two Pointers         ██████████████████████████████████████          ★★★★
Sliding Window       ████████████████████████████████████████████    ★★★★
Binary Search        ███████████████████████████████                 ★★★
Stacks/Queues        ██████████████████████████████████████          ★★★★
Linked Lists         █████████████████████████                      ★★★
Trees                ████████████████████████████████                ★★★
Heaps                █████████████████                              ★★
Graphs               ████████████████                               ★★
DP                   ██████████                                     ★
Greedy               ████████████████████                           ★★
Backtracking         ████████████████                               ★★
Tries                ██████                                         ★
Bit Manipulation     ████████████████████                           ★★

→ IMMEDIATE FOCUS: DP, Tries, Heaps
→ SECONDARY FOCUS: Graphs, Backtracking, Bit Manipulation
→ MAINTAIN: Arrays, Hashing, Sliding Window
🎯 The Pattern Mastery Matrix
Track not just WHAT you've solved, but HOW WELL you understand each pattern across difficulty levels.

text

╔═══════════════════════════════════════════════════════════════════╗
║                   PATTERN MASTERY MATRIX                         ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                   ║
║  Pattern           │ Easy      │ Medium    │ Hard      │ Overall  ║
║  ──────────────────┼───────────┼───────────┼───────────┼────────  ║
║  Sliding Window    │ 8/8 ✅    │ 6/8 🟢   │ 1/3 🟡   │ ★★★★   ║
║  Two Pointers      │ 5/5 ✅    │ 7/9 🟢   │ 2/4 🟡   │ ★★★★   ║
║  Binary Search     │ 4/4 ✅    │ 5/10 🟡  │ 0/3 🔴   │ ★★★    ║
║  Hashing           │ 6/6 ✅    │ 8/10 🟢  │ 2/3 🟢   │ ★★★★   ║
║  Stack/Queue       │ 5/5 ✅    │ 4/8 🟡   │ 1/3 🔴   │ ★★★    ║
║  Trees             │ 6/7 🟢   │ 5/12 🟡  │ 0/5 🔴   │ ★★     ║
║  Graphs            │ 3/4 🟢   │ 3/10 🔴  │ 0/5 🔴   │ ★★     ║
║  DP                │ 4/5 🟢   │ 3/15 🔴  │ 0/8 🔴   │ ★      ║
║  Greedy            │ 3/4 🟢   │ 4/8 🟡   │ 0/3 🔴   │ ★★★    ║
║  Backtracking      │ 2/3 🟢   │ 2/6 🔴   │ 0/4 🔴   │ ★★     ║
║                                                                   ║
║  FORMAT: Solved/Attempted  Status                                 ║
║  🟢 80%+  🟡 50-79%  🔴 <50%                                    ║
║                                                                   ║
╚═══════════════════════════════════════════════════════════════════╝
How to Use the Matrix
text

READING THE MATRIX:

1. ROWS tell you which PATTERNS need work
   → DP row is mostly 🔴 → need dedicated DP practice

2. COLUMNS tell you which DIFFICULTY LEVEL is your ceiling
   → Hard column is mostly 🔴 → mediums are your current level
   → That's FINE — master mediums before attempting hards

3. DIAGONAL PROGRESS is the goal
   → First get all Easy to 🟢
   → Then get all Medium to 🟢
   → Then tackle Hards

4. DON'T move to Hard until Medium is 🟢
   → Building on shaky foundations wastes time
   → 🟢 in Medium = ready for Hard in that pattern
⚡ The Confidence Meter
Self-assessment of your confidence for each topic. Update every 2 weeks.

text

╔══════════════════════════════════════════════════════════════════╗
║                     CONFIDENCE METER                             ║
║           "If this appeared in my interview tomorrow,            ║
║            how confident am I?"                                  ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║  TOPIC              │ CONFIDENCE │ REASON                        ║
║  ───────────────────┼────────────┼─────────────────────────────  ║
║  Arrays             │ 😊 90%     │ Strong fundamentals, many     ║
║                     │            │ problems solved               ║
║  ───────────────────┼────────────┼─────────────────────────────  ║
║  Hashing            │ 😊 85%     │ Comfortable with maps/sets    ║
║                     │            │ and counting patterns         ║
║  ───────────────────┼────────────┼─────────────────────────────  ║
║  Sliding Window     │ 🙂 75%    │ Fixed window: strong          ║
║                     │            │ Variable window: needs work   ║
║  ───────────────────┼────────────┼─────────────────────────────  ║
║  Binary Search      │ 🙂 70%    │ Standard BS is fine, but      ║
║                     │            │ BS on answer space is shaky   ║
║  ───────────────────┼────────────┼─────────────────────────────  ║
║  Trees              │ 😐 55%    │ Traversals ok, but BST        ║
║                     │            │ operations and tree DP weak   ║
║  ───────────────────┼────────────┼─────────────────────────────  ║
║  Graphs             │ 😐 45%    │ BFS/DFS ok, but Dijkstra      ║
║                     │            │ and topological sort unclear  ║
║  ───────────────────┼────────────┼─────────────────────────────  ║
║  DP                 │ 😤 25%    │ Can follow solutions but      ║
║                     │            │ can't derive recurrence       ║
║  ───────────────────┼────────────┼─────────────────────────────  ║
║  Backtracking       │ 😤 30%    │ Know the template but         ║
║                     │            │ struggle with pruning         ║
║  ───────────────────┼────────────┼─────────────────────────────  ║
║                                                                  ║
║  CONFIDENCE LEVELS:                                              ║
║    😊 80-100% → "Bring it on" — interview ready                ║
║    🙂 60-79%  → "I can handle most" — needs some practice      ║
║    😐 40-59%  → "Hit or miss" — needs focused work             ║
║    😤 0-39%   → "I'd panic" — needs dedicated study            ║
║                                                                  ║
╚══════════════════════════════════════════════════════════════════╝
How Confidence Meter Guides Your Study
text

RULE: Spend time INVERSELY proportional to confidence.

  😤 25% confidence in DP → Spend 30% of your time on DP
  😐 45% confidence in Graphs → Spend 20% on Graphs
  😊 90% confidence in Arrays → Spend 5% maintaining Arrays

THE FORMULA:
  Study Priority = (100 - Confidence) × (Frequency in Interviews)

  DP: (100-25) × HIGH = HIGHEST PRIORITY
  Graphs: (100-45) × HIGH = HIGH PRIORITY
  Backtracking: (100-30) × MEDIUM = MEDIUM PRIORITY
  Arrays: (100-90) × HIGH = LOW PRIORITY (already strong)
📓 The Mistake Journal
Your mistakes are your best teachers — but only if you REMEMBER them.

text

╔══════════════════════════════════════════════════════════════╗
║                     MISTAKE JOURNAL                          ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  MISTAKE CATEGORIES:                                         ║
║                                                              ║
║  🔴 CONCEPTUAL — Didn't understand the approach              ║
║  🟠 PATTERN — Failed to recognize the right pattern          ║
║  🟡 IMPLEMENTATION — Logic error while coding                ║
║  🔵 EDGE CASE — Missed a boundary condition                  ║
║  🟣 COMPLEXITY — Wrong time/space analysis                   ║
║  ⚪ SILLY — Typo, wrong variable, off-by-one                ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
Mistake Log Template
text

┌──────────────────────────────────────────────────────────────────┐
│ MISTAKE ENTRY #___                                               │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│ Date:        _______________                                     │
│ Problem:     _______________                                     │
│ Category:    🔴 🟠 🟡 🔵 🟣 ⚪                                  │
│                                                                  │
│ What I did wrong:                                                │
│ _______________________________________________________________  │
│ _______________________________________________________________  │
│                                                                  │
│ What I should have done:                                         │
│ _______________________________________________________________  │
│ _______________________________________________________________  │
│                                                                  │
│ Root cause:                                                      │
│ _______________________________________________________________  │
│                                                                  │
│ How to prevent this in the future:                               │
│ _______________________________________________________________  │
│                                                                  │
│ Have I made this mistake before?  YES / NO                       │
│ If YES, how many times? ___                                      │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
Common Recurring Mistakes to Watch For
text

TOP 10 RECURRING MISTAKES:

1. OFF-BY-ONE ERRORS
   → Using < instead of <=
   → Array index out of bounds
   → Loop running one too many or too few times
   PREVENTION: Always ask "inclusive or exclusive?" for every bound

2. NOT HANDLING EMPTY INPUT
   → Function crashes on empty array/string
   PREVENTION: Always add empty check as first line

3. INTEGER OVERFLOW
   → Multiplying two large ints without using long
   → Sum exceeding int range
   PREVENTION: Use long/long long when values can exceed 10^9

4. WRONG INITIAL VALUE
   → Initialize max to 0 when values can be negative
   → Initialize min to 0 when values can be large
   PREVENTION: Use -infinity for max, +infinity for min

5. MODIFYING COLLECTION WHILE ITERATING
   → Removing elements from list while looping over it
   PREVENTION: Iterate over a copy, or collect indices to remove

6. FORGETTING TO RESET STATE
   → In backtracking, forgetting to undo a choice
   → In multiple test cases, not resetting variables
   PREVENTION: Code the "undo" step RIGHT AFTER the "do" step

7. CONFUSING INDICES AND VALUES
   → Using arr[arr[i]] when you meant arr[i]
   → Mixing up "position" and "value" in your thinking
   PREVENTION: Name variables clearly: "index" vs "value"

8. WRONG COMPARISON FOR OBJECTS
   → Using == instead of .equals() (Java)
   → Comparing references instead of values
   PREVENTION: Know your language's comparison rules

9. NOT CONSIDERING DUPLICATES
   → Assuming all elements are unique when they're not
   → Counting the same pair twice
   PREVENTION: Always ask "can there be duplicates?"

10. GREEDY WHEN IT SHOULD BE DP
    → Assuming local optimal = global optimal without proof
    → Finding a counterexample later
    PREVENTION: Try to find a counterexample for greedy before coding
Mistake Frequency Tracker
text

Track how often each mistake type occurs:

  ┌──────────────────┬─────┬─────┬─────┬─────┬─────┐
  │ Mistake Type     │ W1  │ W2  │ W3  │ W4  │Trend│
  ├──────────────────┼─────┼─────┼─────┼─────┼─────┤
  │ Off-by-one       │ III │ II  │ I   │ I   │ ↓ ✅│
  │ Empty input      │ II  │ II  │ I   │ 0   │ ↓ ✅│
  │ Wrong pattern    │ III │ III │ II  │ II  │ ↓   │
  │ No plan before   │ II  │ I   │ I   │ 0   │ ↓ ✅│
  │ coding           │     │     │     │     │     │
  │ Overflow         │ I   │ I   │ I   │ I   │ → 🟡│
  └──────────────────┴─────┴─────┴─────┴─────┴─────┘

  ↓ = Improving   → = Flat (needs attention)   ↑ = Getting worse
💎 The Key Insight Notebook
Collect the "aha" moments. These are the distilled wisdom that makes you better.

The Insight Template
text

╔══════════════════════════════════════════════════════════════╗
║                     KEY INSIGHT                              ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  Date:       _______________                                 ║
║  Problem:    _______________                                 ║
║  Pattern:    _______________                                 ║
║                                                              ║
║  THE INSIGHT:                                                ║
║  ___________________________________________________________║
║  ___________________________________________________________║
║  ___________________________________________________________║
║                                                              ║
║  WHY IT WORKS:                                               ║
║  ___________________________________________________________║
║  ___________________________________________________________║
║                                                              ║
║  WHERE ELSE CAN I APPLY THIS:                                ║
║  ___________________________________________________________║
║  ___________________________________________________________║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
Example Insights Collection
text

INSIGHT #1 — The Complement Trick
  Pattern: Hashing
  Insight: "Instead of searching for a PAIR that sums to target,
           search for the COMPLEMENT (target - current) in a hash map.
           This turns O(n²) into O(n)."
  Applies to: Two Sum, Pair with difference, Subarray sum = K

INSIGHT #2 — Sort to Reveal Structure
  Pattern: Sorting + Greedy
  Insight: "When the problem involves intervals, meetings, or ranges,
           SORTING by start time (or end time) almost always simplifies things.
           After sorting, you only need to compare adjacent elements."
  Applies to: Merge intervals, Meeting rooms, Non-overlapping intervals

INSIGHT #3 — Binary Search on Answer Space
  Pattern: Binary Search
  Insight: "If the problem asks 'what is the minimum X such that
           condition Y is satisfied', and the condition is MONOTONIC
           (if X works, X+1 also works), binary search on X.
           For each candidate X, CHECK if it's feasible in O(n)."
  Applies to: Koko eating bananas, Split array largest sum,
              Minimum days to make bouquets

INSIGHT #4 — Track From Both Ends
  Pattern: Prefix/Suffix
  Insight: "When you need information from BOTH left and right of
           each element, do TWO passes: one forward, one backward.
           Precompute prefix (left→right) and suffix (right→left) arrays."
  Applies to: Product except self, Trapping rain water,
              Best time to buy and sell stock

INSIGHT #5 — DP State = What Info Do I Need to Make the Next Decision?
  Pattern: Dynamic Programming
  Insight: "The hardest part of DP is defining the STATE.
           Ask: 'If I'm at position i, what ADDITIONAL information
           do I need to decide what to do next?'
           That additional information becomes the other dimensions of dp."
  Applies to: ALL DP problems

INSIGHT #6 — BFS = Shortest in Unweighted, Dijkstra = Shortest in Weighted
  Pattern: Graphs
  Insight: "If edges have no weights (or all weight = 1), BFS gives
           shortest path. If edges have different weights, use Dijkstra.
           NEVER use DFS for shortest path."
  Applies to: Grid shortest path, Word ladder, Network delay time

INSIGHT #7 — Monotonic Stack = Next Greater/Smaller
  Pattern: Stack
  Insight: "Whenever the problem asks for the NEXT GREATER or
           NEXT SMALLER element for each position, use a monotonic stack.
           Process elements and maintain the stack in increasing
           (for next greater) or decreasing (for next smaller) order."
  Applies to: Next greater element, Daily temperatures,
              Largest rectangle in histogram
Building Your Insight Collection Over Time
text

MONTH 1: ~10-15 insights (basic patterns)
MONTH 2: ~25-30 insights (intermediate tricks)  
MONTH 3: ~40-50 insights (combinations and variations)
MONTH 6: ~80-100 insights (your personal DSA bible)

REVIEW your insight notebook:
  → Before every contest
  → Before every interview
  → Weekly during practice sessions
  → It becomes your MOST valuable resource
🏆 Contest & Mock Interview Tracker
Contest Tracker
text

┌───────────────────────────────────────────────────────────────────────┐
│                        CONTEST LOG                                    │
├──────┬────────────┬──────────┬────────┬────────┬─────────┬───────────┤
│  #   │ Date       │ Platform │ Type   │Problems│ Solved  │ Rank /    │
│      │            │          │        │ Count  │         │ Rating    │
├──────┼────────────┼──────────┼────────┼────────┼─────────┼───────────┤
│  1   │ 2024-01-20 │LeetCode  │Weekly  │  4     │ 2/4     │ 8432/     │
│      │            │          │Contest │        │         │ 25000     │
├──────┼────────────┼──────────┼────────┼────────┼─────────┼───────────┤
│  2   │ 2024-01-21 │Codeforces│Div 2   │  6     │ 3/6     │ 1245      │
│      │            │          │        │        │ (A,B,C) │ (+45)     │
└──────┴────────────┴──────────┴────────┴────────┴─────────┴───────────┘

POST-CONTEST ANALYSIS (fill for EVERY contest):

  Problems I SOLVED:
    → Q1: [technique] — solved in [time]
    → Q2: [technique] — solved in [time]

  Problems I DIDN'T solve:
    → Q3: [why I failed] — [what technique was needed]
    → Q4: [why I failed] — [what technique was needed]

  UPSOLVING (solving unsolved problems after contest):
    → Q3: □ Upsolved on [date]  □ Added to revision list
    → Q4: □ Upsolved on [date]  □ Added to revision list

  LESSONS:
    → _______________________________________________
    → _______________________________________________
Mock Interview Tracker
text

┌──────────────────────────────────────────────────────────────────────────┐
│                      MOCK INTERVIEW LOG                                  │
├────┬────────────┬───────────┬──────────┬──────────┬──────────┬──────────┤
│ #  │ Date       │ With Whom │ Problem  │ Result   │ Feedback │ Action   │
│    │            │           │ Given    │          │ Received │ Items    │
├────┼────────────┼───────────┼──────────┼──────────┼──────────┼──────────┤
│ 1  │ 2024-02-01 │ Pramp     │ Matrix   │ Solved   │ "Good    │ Practice │
│    │            │           │ rotation │ with     │ approach │ talking  │
│    │            │           │          │ hints    │ but went │ while    │
│    │            │           │          │          │ silent   │ coding   │
│    │            │           │          │          │ while    │          │
│    │            │           │          │          │ coding"  │          │
├────┼────────────┼───────────┼──────────┼──────────┼──────────┼──────────┤
│ 2  │ 2024-02-05 │ Friend    │ LRU      │ Could    │ "Didn't  │ Study    │
│    │            │ (John)    │ Cache    │ not      │ clarify  │ design   │
│    │            │           │          │ solve    │ require- │ pattern  │
│    │            │           │          │          │ ments"   │ problems │
└────┴────────────┴───────────┴──────────┴──────────┴──────────┴──────────┘

MOCK INTERVIEW SELF-ASSESSMENT:

  Communication:     ☆☆☆☆☆  /5
  Problem Solving:   ☆☆☆☆☆  /5
  Code Quality:      ☆☆☆☆☆  /5
  Edge Cases:        ☆☆☆☆☆  /5
  Time Management:   ☆☆☆☆☆  /5
  Handling Pressure:  ☆☆☆☆☆  /5

  What went well:    ___________________________________
  What to improve:   ___________________________________
  
  TARGET: Do at least 2 mock interviews per month
🛠️ Tools & Where to Maintain Your Log
Option 1 — Spreadsheet (Recommended for Most People)
text

WHY SPREADSHEETS:
  ✅ Easy to filter, sort, and search
  ✅ Can create charts and visualizations
  ✅ Auto-calculate statistics
  ✅ Access from any device (Google Sheets)
  ✅ Can share with study partners

RECOMMENDED STRUCTURE:
  → Tab 1: Problem Log (core tracking)
  → Tab 2: Revision Tracker (spaced repetition)
  → Tab 3: Weekly Reviews
  → Tab 4: Monthly Reviews
  → Tab 5: Mistake Journal
  → Tab 6: Key Insights
  → Tab 7: Contest Log
  → Tab 8: Dashboard (charts and summary stats)

GOOGLE SHEETS TIPS:
  → Use Data Validation for Status column (dropdown: ✅ 🔶 ❌ 🔁)
  → Use COUNTIF to auto-calculate topic-wise stats
  → Use Conditional Formatting (green for ✅, red for ❌)
  → Use FILTER function for "due revisions today"
  → Pin the header row
Option 2 — Notion
text

WHY NOTION:
  ✅ Beautiful templates and databases
  ✅ Relational databases (link problems to topics)
  ✅ Multiple views (table, board, calendar, gallery)
  ✅ Built-in formulas and rollups
  ✅ Great for the insight journal (rich text)

RECOMMENDED STRUCTURE:
  → Database 1: Problems (with properties for all columns)
  → Database 2: Topics (linked to Problems)
  → Database 3: Reviews (weekly/monthly templates)
  → Database 4: Insights (rich text with examples)
  → View: Calendar view for revision scheduling
  → View: Board view organized by topic
  → View: Gallery view for key insights
Option 3 — GitHub Repository
text

WHY GITHUB:
  ✅ Version controlled
  ✅ Markdown files are clean and readable
  ✅ Shows commitment to potential employers
  ✅ Can include solution files alongside logs
  ✅ Free and accessible

RECOMMENDED STRUCTURE:
  dsa-journey/
  ├── README.md (overview + stats)
  ├── problem-log.md (or .csv)
  ├── weekly-reviews/
  │   ├── week-01.md
  │   ├── week-02.md
  │   └── ...
  ├── monthly-reviews/
  │   ├── month-01.md
  │   └── ...
  ├── insights/
  │   ├── sliding-window.md
  │   ├── dynamic-programming.md
  │   └── ...
  ├── mistakes/
  │   └── mistake-journal.md
  └── solutions/
      ├── arrays/
      ├── trees/
      ├── dp/
      └── ...
Option 4 — Physical Notebook
text

WHY PHYSICAL:
  ✅ No distractions
  ✅ Writing by hand improves retention (proven by research)
  ✅ Tactile satisfaction of checking things off
  ✅ Always available (no battery, no wifi)

LIMITATIONS:
  ❌ Can't search or filter
  ❌ Can't auto-calculate stats
  ❌ Can't easily share
  ❌ Harder to reorganize

RECOMMENDATION:
  → Use a physical notebook for the INSIGHT JOURNAL and MISTAKE LOG
  → Use a digital tool for the PROBLEM LOG and REVISION TRACKER
  → Best of both worlds
Option 5 — Dedicated Apps and Websites
text

LEETCODE BUILT-IN:
  → LeetCode tracks your solved problems, streaks, and topic distribution
  → Use the "Lists" feature to create topic-specific lists
  → Use the "Notes" feature for key insights per problem
  → LIMITATION: No revision scheduling, no custom tracking

CODOLIO / LEETCODE TRACKER EXTENSIONS:
  → Browser extensions that enhance LeetCode tracking
  → Auto-capture solve data
  → Visualizations and heatmaps

ANKI (for revision):
  → Flashcard app with built-in spaced repetition
  → Create a card for each problem's key insight
  → Front: Problem statement
  → Back: Approach + key insight + complexity
  → The app schedules reviews automatically
📝 Sample Filled Log — 2 Weeks Example
Week 1 Problem Log
text

┌────┬────────────┬─────────────────────┬────────┬──────┬──────────────┬──────┬──────┐
│ #  │ Date       │ Problem             │Platform│ Diff │ Pattern      │Status│ Time │
├────┼────────────┼─────────────────────┼────────┼──────┼──────────────┼──────┼──────┤
│  1 │ 2024-01-15 │ Two Sum             │LC #1   │ Easy │ Hashing      │  ✅  │ 12m  │
│  2 │ 2024-01-15 │ Valid Parentheses   │LC #20  │ Easy │ Stack        │  ✅  │ 8m   │
│  3 │ 2024-01-15 │ 3Sum                │LC #15  │ Med  │ Two Pointers │  🔶  │ 45m  │
│  4 │ 2024-01-16 │ Max Subarray        │LC #53  │ Med  │ DP/Kadane    │  ✅  │ 15m  │
│  5 │ 2024-01-16 │ LCA of BST          │LC #235 │ Med  │ Tree/DFS     │  ❌  │ 50m  │
│  6 │ 2024-01-17 │ LCA of BST (REDO)   │LC #235 │ Med  │ Tree/DFS     │  🔁✅│ 12m  │
│  7 │ 2024-01-17 │ Merge Intervals     │LC #56  │ Med  │ Sort+Greedy  │  ✅  │ 22m  │
│  8 │ 2024-01-17 │ Group Anagrams      │LC #49  │ Med  │ Hashing      │  ✅  │ 18m  │
│  9 │ 2024-01-18 │ 3Sum (REVISION)     │LC #15  │ Med  │ Two Pointers │  🔁🔶│ 30m  │
│ 10 │ 2024-01-18 │ Longest Substr w/o  │LC #3   │ Med  │ Sliding Win  │  🔶  │ 35m  │
│    │            │ Repeating Chars     │        │      │              │      │      │
│ 11 │ 2024-01-19 │ Binary Search       │LC #704 │ Easy │ Binary Search│  ✅  │ 5m   │
│ 12 │ 2024-01-19 │ Search Rotated Arr  │LC #33  │ Med  │ Binary Search│  ❌  │ 45m  │
│ 13 │ 2024-01-20 │ Search Rotated(REDO)│LC #33  │ Med  │ Binary Search│  🔁🔶│ 20m  │
│ 14 │ 2024-01-20 │ Number of Islands   │LC #200 │ Med  │ Graph/DFS    │  ✅  │ 20m  │
│ 15 │ 2024-01-21 │ LCA of BST(Rev 2)   │LC #235 │ Med  │ Tree/DFS     │  🔁✅│ 8m   │
│ 16 │ 2024-01-21 │ Coin Change         │LC #322 │ Med  │ DP           │  ❌  │ 55m  │
└────┴────────────┴─────────────────────┴────────┴──────┴──────────────┴──────┴──────┘
Week 1 Key Insights Captured
text

INSIGHT from #3 (3Sum):
  "After sorting, skip duplicate values for the first element
   AND for the two-pointer elements to avoid duplicate triplets.
   The skip must happen AFTER finding a valid triplet, not before."

INSIGHT from #5 (LCA of BST):
  "USE the BST property! If both nodes are smaller than root,
   LCA is in the left subtree. If both larger, it's in the right.
   If they split (one left, one right), root IS the LCA."

INSIGHT from #10 (Longest Substring):
  "Variable sliding window: expand right, add to set.
   If duplicate found, shrink left until no duplicate.
   Key: use a hash SET, not just a counter."

INSIGHT from #12 (Search Rotated Array):
  "The trick is: one half is ALWAYS sorted. Check if target
   is in the sorted half. If yes, search there. If no,
   search the other half. This maintains O(log n)."

INSIGHT from #16 (Coin Change):
  "This is unbounded knapsack. dp[amount] = min coins to make amount.
   For each coin, dp[i] = min(dp[i], dp[i-coin] + 1).
   Initialize dp[0] = 0, everything else = infinity."
Week 1 Review (Filled Example)
text

╔══════════════════════════════════════════════════════════════╗
║              WEEKLY REVIEW — Week of Jan 15-21               ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  Total Problems Attempted:     16 (12 new + 4 revisions)     ║
║  Solved Independently (✅):    7  (44%)                      ║
║  Solved with Hints (🔶):       3  (19%)                      ║
║  Could Not Solve (❌):         2  (12%)                      ║
║  Revisions Completed (🔁):     4  (3✅, 1🔶)                ║
║  Total Time Spent:             ~7.5 hours                    ║
║  Average Time per Problem:     ~28 minutes                   ║
║                                                              ║
║  Difficulty: 3 Easy / 13 Medium / 0 Hard                     ║
║                                                              ║
║  Topics: Hashing(3), Two Pointers(2), Stack(1), DP(2),       ║
║          Tree(3), Sorting(1), Sliding Window(1),             ║
║          Binary Search(3), Graph(1)                          ║
║                                                              ║
║  WHAT WENT WELL:                                             ║
║  → Hashing problems feel natural now                         ║
║  → Revision system is working — LCA went ❌→✅ in 5 days    ║
║  → Merge Intervals clicked immediately                       ║
║                                                              ║
║  WHAT DIDN'T GO WELL:                                        ║
║  → DP still feels like guesswork (Coin Change)               ║
║  → Binary Search on modified arrays is confusing             ║
║  → Spent too long on problems before accepting I was stuck   ║
║                                                              ║
║  RECURRING MISTAKES:                                         ║
║  → Not using BST properties (trying generic tree approaches) ║
║  → Going silent while solving — need to talk through it      ║
║                                                              ║
║  PLAN FOR NEXT WEEK:                                         ║
║  → Focus: 5 more Binary Search problems (including BS on     ║
║    answer space)                                             ║
║  → Focus: 3 easy DP problems to build foundation             ║
║  → Revision: 3Sum, Search Rotated, Coin Change               ║
║  → Target: 12-15 problems                                    ║
║  → Goal: Practice talking out loud while solving             ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
🚫 The Anti-Patterns — Tracking Mistakes to Avoid
Anti-Pattern 1: Over-Tracking
text

THE PROBLEM:
  → Spending 20 minutes documenting a problem you solved in 10 minutes
  → Tracking becomes a chore that kills motivation
  → Analysis paralysis — too much data, no action

THE FIX:
  → The 2-minute rule: if logging takes more than 2 minutes, you're overdoing it
  → Only the CORE columns are mandatory
  → Extended columns are for problems that TAUGHT you something
  → Better to track consistently with less detail than 
    perfectly for 2 weeks then stop
Anti-Pattern 2: Vanity Metrics
text

THE PROBLEM:
  → "I solved 500 problems!" (but 400 were easy and you can't remember any)
  → Counting quantity without quality
  → Doing easy problems to feel good about the numbers

THE FIX:
  → Track INDEPENDENCE RATE, not just count
  → Track DIFFICULTY DISTRIBUTION (target: 20% easy, 60% medium, 20% hard)
  → Track REVISION SUCCESS rate
  → A person who solved 200 problems with deep understanding beats 
    someone who "solved" 500 by looking at answers
Anti-Pattern 3: Not Being Honest
text

THE PROBLEM:
  → Marking 🔶 as ✅ because "I ALMOST had it"
  → Not logging ❌ problems at all
  → Inflating your confidence meter

THE FIX:
  → The log is for YOU, not for anyone else
  → Lying to your log = lying to yourself
  → ❌ is not failure — it's a LEARNING OPPORTUNITY
  → The most valuable entries in your log are the ❌ ones
  → Be ruthlessly honest: if you looked at ANY hint, it's 🔶
Anti-Pattern 4: Tracking Without Reviewing
text

THE PROBLEM:
  → You have a beautiful spreadsheet with 200 entries
  → You've never once looked back at it
  → Data without analysis is just noise

THE FIX:
  → Weekly review is NON-NEGOTIABLE (30 min/week)
  → Monthly review catches long-term trends
  → If you're not going to review, don't bother tracking
  → The VALUE is in the REVIEW, not the RECORDING
Anti-Pattern 5: Skipping Revisions
text

THE PROBLEM:
  → "I'll revise later" (you won't)
  → Solving new problems feels more productive than revising old ones
  → 3 months in, you can't solve problems you "solved" before

THE FIX:
  → Revisions FIRST, new problems SECOND
  → Block 15-20 minutes daily for revisions
  → If your revision queue has 10+ overdue items, 
    STOP solving new problems until you catch up
  → Solving 100 problems you remember > 300 problems you forgot
Anti-Pattern 6: Giving Up on the System
text

THE PROBLEM:
  → You miss a few days of logging
  → You feel behind and guilty
  → You abandon the entire system

THE FIX:
  → Missing a few days is NORMAL
  → Just pick up where you left off
  → Don't try to backfill — just start fresh from today
  → The system serves YOU — you don't serve the system
  → A imperfect system used consistently > a perfect system abandoned
✅ Printable Checklists
Daily Checklist
text

╔══════════════════════════════════════════════════════╗
║              DAILY DSA CHECKLIST                     ║
║              Date: _______________                   ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  □ Reviewed revision queue                           ║
║  □ Completed ___ due revisions                       ║
║  □ Solved ___ new problems                           ║
║  □ Logged all problems in problem log                ║
║  □ Wrote key insights for today's problems           ║
║  □ Recorded any mistakes in mistake journal          ║
║  □ Set revisit dates for today's problems            ║
║  □ Planned tomorrow's focus                          ║
║                                                      ║
║  Today's wins: _________________________________     ║
║  Today's struggle: ______________________________    ║
║                                                      ║
╚══════════════════════════════════════════════════════╝
Weekly Checklist
text

╔══════════════════════════════════════════════════════╗
║              WEEKLY DSA CHECKLIST                    ║
║              Week of: _______________                ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  □ Completed weekly review template                  ║
║  □ Calculated this week's solve rate                 ║
║  □ Calculated this week's independence rate          ║
║  □ Identified weakest topic this week                ║
║  □ Reviewed mistake journal for recurring mistakes   ║
║  □ Re-read key insights from this week               ║
║  □ Set specific goals for next week                  ║
║  □ Checked if on track for monthly target            ║
║  □ Participated in at least 1 contest (optional)     ║
║  □ Updated pattern mastery matrix                    ║
║                                                      ║
╚══════════════════════════════════════════════════════╝
Monthly Checklist
text

╔══════════════════════════════════════════════════════╗
║              MONTHLY DSA CHECKLIST                   ║
║              Month: _______________                  ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  □ Completed monthly review template                 ║
║  □ Updated pattern mastery matrix                    ║
║  □ Updated confidence meter for all topics           ║
║  □ Compared metrics with last month                  ║
║  □ Analyzed mistake frequency trends                 ║
║  □ Identified top 3 focus areas for next month       ║
║  □ Re-read ALL key insights (30-min session)         ║
║  □ Done at least 2 mock interviews this month        ║
║  □ Updated skill gap map                             ║
║  □ Celebrated progress (you deserve it!) 🎉          ║
║                                                      ║
║  Am I on track for my goal?                          ║
║  □ YES — keep going!                                 ║
║  □ NO — what needs to change? ___________________    ║
║                                                      ║
╚══════════════════════════════════════════════════════╝
Pre-Interview Checklist
text

╔══════════════════════════════════════════════════════╗
║            PRE-INTERVIEW PREPARATION                 ║
║            Date: _______________                     ║
║            Company: _______________                  ║
╠══════════════════════════════════════════════════════╣
║                                                      ║
║  ONE WEEK BEFORE:                                    ║
║  □ Reviewed all key insights in notebook             ║
║  □ Re-solved top 20 most important problems          ║
║  □ Practiced 2-3 mock interviews                     ║
║  □ Reviewed company-tagged problems on LeetCode      ║
║  □ Reviewed common mistake journal entries           ║
║                                                      ║
║  ONE DAY BEFORE:                                     ║
║  □ Reviewed the 15 core patterns (quick summary)     ║
║  □ Reviewed constraint → complexity mapping          ║
║  □ Reviewed the UMPIRE framework                     ║
║  □ Practiced talking through 2 problems out loud     ║
║  □ Prepared questions to ask the interviewer         ║
║  □ Got good sleep                                    ║
║                                                      ║
║  RIGHT BEFORE:                                       ║
║  □ Deep breaths — you've prepared for this           ║
║  □ Remember: communicate, think out loud, stay calm  ║
║  □ It's a conversation, not an exam                  ║
║  □ They're rooting for you                           ║
║  □ You've got this 💪                                ║
║                                                      ║
╚══════════════════════════════════════════════════════╝
🏁 The Complete System Summary
text

╔══════════════════════════════════════════════════════════════╗
║           YOUR DSA TRACKING SYSTEM — SUMMARY                 ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  📋 PROBLEM LOG                                              ║
║     → Every problem, every attempt, logged honestly          ║
║     → Core columns + extended columns for learning           ║
║     → 2-minute post-solve ritual                             ║
║                                                              ║
║  📅 DAILY LOG                                                ║
║     → Quick snapshot: count, time, mood                      ║
║     → Best moment + struggle point                           ║
║     → Tomorrow's plan                                        ║
║                                                              ║
║  📆 WEEKLY REVIEW (30 min)                                   ║
║     → Numbers, topic breakdown, reflection                   ║
║     → Solve rate, independence rate, average time             ║
║     → Next week's plan                                       ║
║                                                              ║
║  📊 MONTHLY REVIEW (1 hour)                                  ║
║     → Big picture progress comparison                        ║
║     → Pattern mastery assessment                             ║
║     → Strategy adjustment                                    ║
║                                                              ║
║  🔁 REVISION SYSTEM                                          ║
║     → Spaced repetition: +1, +3, +7, +14, +30 days          ║
║     → Revisions first, new problems second                   ║
║     → Track revision success/failure                         ║
║                                                              ║
║  🔍 WEAKNESS TRACKER                                         ║
║     → Topic-wise solve rates                                 ║
║     → Skill gap map visualization                            ║
║     → Action plans for weak areas                            ║
║                                                              ║
║  🎯 PATTERN MASTERY MATRIX                                   ║
║     → Difficulty × pattern grid                              ║
║     → Track readiness for each pattern at each level         ║
║                                                              ║
║  📓 MISTAKE JOURNAL                                          ║
║     → Categorized mistakes with root cause                   ║
║     → Frequency tracking to spot recurring errors            ║
║     → Prevention strategies                                  ║
║                                                              ║
║  💎 KEY INSIGHT NOTEBOOK                                     ║
║     → "Aha" moments captured and organized                   ║
║     → Your personal DSA bible                                ║
║     → Review before contests and interviews                  ║
║                                                              ║
║  🏆 CONTEST & MOCK TRACKER                                   ║
║     → Performance trends over time                           ║
║     → Post-contest analysis and upsolving                    ║
║     → Interview simulation feedback                          ║
║                                                              ║
║  ──────────────────────────────────────────────────────────   ║
║                                                              ║
║  THE GOLDEN RULES:                                           ║
║                                                              ║
║  1. Consistency > Perfection                                 ║
║     An imperfect log maintained daily beats a perfect        ║
║     log abandoned after a week.                              ║
║                                                              ║
║  2. Honesty > Ego                                            ║
║     Every ❌ is a future ✅ waiting to happen.               ║
║     Only if you're honest about it.                          ║
║                                                              ║
║  3. Review > Record                                          ║
║     The value is in LOOKING BACK at your data,               ║
║     not in writing it down.                                  ║
║                                                              ║
║  4. Revise > Solve New                                       ║
║     100 problems you remember forever >                      ║
║     500 problems you've forgotten.                           ║
║                                                              ║
║  5. The System Serves You                                    ║
║     Adapt it. Simplify it. Make it yours.                    ║
║     If something doesn't help, drop it.                      ║
║     If something's missing, add it.                          ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
⭐ Star this repo if this system helps you stay on track. Share it with your study group — accountability partners make all the difference.

