# Two Sum Problem

## Problem Statement
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

**Constraints:**
- Each input has exactly one solution.
- You may not use the same element twice.
- You can return the answer in any order.

**Example 1:**
Input: nums =, target = 9
Output:
Explanation: nums + nums == 9[2][7][11][15][0][1]
**Example 2:**
Input: nums =, target = 6
Output:[3][2][4][1]
**Example 3:**
Input: nums =, target = 6
Output:[3][0][1]

## Approach: One-Pass HashMap
We use a `HashMap` to store each number and its index as we iterate. For every element `nums[i]`, we check if `target - nums[i]` already exists in the map.

**Why it works:**
If `x + y = target`, then when we reach `y`, we will have already stored `x` with its index. So we can return both indices immediately.

**Time Complexity:** `O(n)`
We traverse the array only once. HashMap `get` and `put` operations are `O(1)` on average.

**Space Complexity:** `O(n)`
In the worst case, we store all `n` elements in the HashMap.

## Code
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> numToIndex = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];

            if (numToIndex.containsKey(complement)) {
                return new int[] { numToIndex.get(complement), i };
            }

            numToIndex.put(nums[i], i);
        }

        // Won't reach here per problem constraints
        return new int[] {};
    }
}