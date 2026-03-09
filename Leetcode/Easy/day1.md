# 🏆 Leetcode Problem #1: Two Sum (Problem #1)

```
PROBLEM:
════════
Given an array of integers nums and an integer target,
return INDICES of the two numbers that add up to target.

Example:
  Input:  nums = [2, 7, 11, 15], target = 9
  Output: [0, 1]
  Why?    nums[0] + nums[1] = 2 + 7 = 9

Rules:
  - Each input has EXACTLY one solution
  - Can't use same element twice
```

---

## Approach 1: Brute Force — O(n²)

```java
// Leetcode/Easy/day1_TwoSum.java

class Solution {
    public int[] twoSum(int[] nums, int target) {
        // Check every pair
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        return new int[]{}; // No solution found
    }
}

/*
TIME:  O(n²) — Two nested loops
SPACE: O(1)  — No extra space

WHY THIS IS BAD:
If array has 10,000 elements → 100,000,000 operations!
*/
```

---

## Approach 2: Optimal — HashMap — O(n)

```java
import java.util.HashMap;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        // HashMap stores: value → index
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            
            // Check if complement already exists in map
            if (map.containsKey(complement)) {
                return new int[]{map.get(complement), i};
            }
            
            // Store current value and its index
            map.put(nums[i], i);
        }
        
        return new int[]{};
    }
}

/*
TIME:  O(n) — Single pass through array
SPACE: O(n) — HashMap stores up to n elements

DRY RUN:
nums = [2, 7, 11, 15], target = 9

i=0: num=2,  complement=9-2=7,  map={} → 7 not in map → map={2:0}
i=1: num=7,  complement=9-7=2,  map={2:0} → 2 IS in map! 
     → return [map.get(2), 1] = [0, 1] ✅

OPTIMIZATION:
10,000 elements → only 10,000 operations (vs 100,000,000)
That's 10,000x faster!
*/
```

---

## 📝 Leetcode Day 1 Summary

- **Problem:** Two Sum (#1)
- **Brute Force:** O(n²) — nested loops
- **Optimal:** O(n) — HashMap technique
- **KEY PATTERN:** "Complement search" using HashMap
- **Status:** ✅ SOLVED
