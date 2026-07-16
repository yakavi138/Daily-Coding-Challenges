# Palindrome Number

## Problem
Given an integer `x`, return `true` if `x` is a palindrome, and `false` otherwise.

A palindrome number reads the same forward and backward.

### Examples

**Example 1**
```
Input: x = 121
Output: true
```

**Example 2**
```
Input: x = -121
Output: false
```

**Example 3**
```
Input: x = 10
Output: false
```

---

## Approach

- If the number is negative, it cannot be a palindrome.
- If the number ends with `0` but is not `0`, it cannot be a palindrome.
- Reverse only half of the number to avoid integer overflow.
- Compare the first half with the reversed second half.
- For odd-length numbers, ignore the middle digit before comparing.

---

## Algorithm

1. Check if the number is negative or ends with `0` (except `0` itself). If yes, return `false`.
2. Reverse the last half of the digits.
3. Stop when the reversed half becomes greater than or equal to the remaining half.
4. Compare:
   - `x == reversedHalf` for even-length numbers.
   - `x == reversedHalf / 10` for odd-length numbers.
5. Return the result.

---

## Time Complexity

- **O(log₁₀ n)**

## Space Complexity

- **O(1)**

---

## Java Solution

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0 || (x % 10 == 0 && x != 0)) {
            return false;
        }

        int reversedHalf = 0;
        while (x > reversedHalf) {
            reversedHalf = reversedHalf * 10 + x % 10;
            x /= 10;
        }

        return x == reversedHalf || x == reversedHalf / 10;
    }
}
```