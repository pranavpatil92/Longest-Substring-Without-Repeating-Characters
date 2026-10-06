# Longest Substring Without Repeating Characters

**LeetCode #3 — Medium**

## Problem

Given a string `s`, find the length of the longest substring without repeating characters.

A substring is a contiguous sequence of characters within a string.

### Example

```text
Input:  s = "zxyzxyz"
Output: 3
```

The longest substring without repeating characters is `"xyz"`.

Another example:

```text
Input:  s = "xxxx"
Output: 1
```

---

## Approach

I used the **Sliding Window** technique with a `set`.

The idea is to maintain a window containing only unique characters.

### Variables

- `left` — left boundary of the current window
- `right` — right boundary of the current window
- `st` — stores the characters currently inside the window
- `maxLen` — stores the maximum length found so far

### How it works

1. Start `left` at `0`.
2. Move `right` from left to right through the string.
3. If `s[right]` is already present in the set, there is a duplicate.
4. Remove characters from the left side of the window until the duplicate is removed.
5. Insert `s[right]` into the set.
6. Calculate the current window length:

```cpp
right - left + 1
```

7. Update `maxLen`.

### Example

For:

```text
s = "zxyz"
```

The window grows:

```text
z
zx
zxy
```

When the second `z` appears, we shrink the window from the left:

```text
zxy → xy
```

Then the new `z` can be added:

```text
xyz
```

The maximum length is `3`.

---

## Complexity

Let `n` be the length of the string.

- **Time:** `O(n log n)`
- **Space:** `O(min(n, character_set_size))`

The `log n` factor comes from using `set`, whose insertion, deletion, and search operations take `O(log n)`.

> Note: This is an accepted solution, but it is not the most optimized implementation. A hash set or character-index approach can achieve `O(n)` time.

---

## C++ Solution

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {

        set<char> st;

        int left = 0;
        int maxLen = 0;

        for (int right = 0; right < s.length(); right++) {

            while (st.find(s[right]) != st.end()) {
                st.erase(s[left]);
                left++;
            }

            st.insert(s[right]);

            maxLen = max(maxLen, right - left + 1);
        }

        return maxLen;
    }
};
```

---

## Submission

- **Language:** C++
- **Status:** Accepted ✅
- **Test Cases:** 1036 / 1036
- **Runtime:** 361 ms
- **Runtime Percentile:** Beats 5.24%
- **Memory:** 131.60 MB
- **Memory Percentile:** Beats 5.34%
- **Submitted:** October 6, 2026

---

## What I Learned

- How to use the `set` container in C++
- How to check whether an element exists using `find()`
- How to remove elements using `erase()`
- How the **Sliding Window** technique works
- How to maintain a window with unique characters
- How to calculate the current window size using:

```cpp
right - left + 1
```

- The difference between an **accepted solution** and an **efficient solution**

---

## Related Problems

- [1695. Maximum Erasure Value](https://leetcode.com/problems/maximum-erasure-value/)
- [2260. Minimum Consecutive Cards to Pick Up](https://leetcode.com/problems/minimum-consecutive-cards-to-pick-up/)
- [2981. Find Longest Special Substring That Occurs Thrice I](https://leetcode.com/problems/find-longest-special-substring-that-occurs-thrice-i/)
