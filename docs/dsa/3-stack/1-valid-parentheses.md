---
layout: default
title: Valid Parentheses
parent: Stack
grand_parent: Data Structures and Algorithms
nav_order: 1
---

# Valid Parentheses

## Problem

Given a string s containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

**Example 1:**

```
Input: s = "()"
Output: true
```

**Example 2:**

```
Input: s = "()[]{}"
Output: true
```

**Example 3:**

```
Input: s = "(]"
Output: false
```

**Constraints:**

- `1 <= s.length <= 104`
- `s` consists of parentheses only `'()[]{}'`.

## Solution

- Stack and HashMap
- Time: O(n)
- Space: O(n)

```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        closeToOpen = {')': "(", "}": "{", ']': '['}

        for c in s:
            if c in closeToOpen:
                if stack and stack[-1] == closeToOpen[c]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(c)

        return not stack
```

## More Information

[Leet Code](https://leetcode.com/problems/valid-parentheses/)
[Neet Code](https://youtu.be/WTzjTskDFMg)
