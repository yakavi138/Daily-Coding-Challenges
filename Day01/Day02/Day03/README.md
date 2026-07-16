# Roman to Integer

## Problem Statement
Convert a Roman numeral to an integer. Roman numerals are represented by seven symbols: `I=1`, `V=5`, `X=10`, `L=50`, `C=100`, `D=500`, `M=1000`.

**Rules:**
1. Usually, numerals are added from left to right.
2. If a smaller value appears before a larger value, subtract it. 
   Example: `IV = 5 - 1 = 4`, `IX = 10 - 1 = 9`

**Constraints:**
- `1 <= s.length <= 15`
- `s` contains only characters `I, V, X, L, C, D, M`
- `s` is a valid Roman numeral in range `[1, 3999]`

**Example 1:**
Input: s = "III"
Output: 3
Explanation: III = 1 + 1 + 1 = 3
**Example 2:**
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V = 5, III = 3

**Example 3:**
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90, IV = 4


## Approach: Left-to-Right with Lookahead
The key insight: If the current symbol is smaller than the next symbol, we subtract it. Otherwise, we add it.

**Steps:**
1. Map each Roman character to its integer value using a `HashMap`.
2. Iterate through the string. For each character:
   - If `current < next`, subtract `current` from result
   - Else, add `current` to result

**Why it works:**  
Roman numerals like `IV` are really `5 - 1`. So when we see `I` and the next char `V` is bigger, we know to do `-1` instead of `+1`.

**Time Complexity:** `O(n)`  
We scan the string once, where `n = s.length()`

**Space Complexity:** `O(1)`  
HashMap has fixed size 7, independent of input size.

## Code
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int romanToInt(String s) {
        Map<Character, Integer> values = new HashMap<>();
        values.put('I', 1);
        values.put('V', 5);
        values.put('X', 10);
        values.put('L', 50);
        values.put('C', 100);
        values.put('D', 500);
        values.put('M', 1000);

        int result = 0;
        
        for (int i = 0; i < s.length(); i++) {
            int current = values.get(s.charAt(i));
            
            // If next char exists and current < next, subtract
            if (i + 1 < s.length() && current < values.get(s.charAt(i + 1))) {
                result -= current;
            } else {
                result += current;
            }
        }
        
        return result;
    }
}