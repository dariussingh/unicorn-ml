---
layout: default
title: Valid Anagram
parent: Arrays & Hashing
grand_parent: Data Structures and Algorithms
nav_order: 2
---

# Valid Anagram

## Problem

Given two strings `s` and `t`, return `true` if `t` is an anagram of s, and `false` otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**

```
Input: s = "rat", t = "car"
Output: false
```

**Constraints:**

- `1 <= s.length, t.length <= 5 * 104`
- `s and t consist of lowercase English letters.`

Follow up: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

## Solution

- HashMap
- Time: O(n)
- Space: O(n)

```python
class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        hashmap_s = {}
        hashmap_t = {}

        for c in s:
            if c not in hashmap_s:
                hashmap_s[c] = 0
            hashmap_s[c] += 1

        for c in t:
            if c not in hashmap_t:
                hashmap_t[c] = 0
            hashmap_t[c] += 1

        return hashmap_s == hashmap_t
```

## More Information

[leet code](https://leetcode.com/problems/valid-anagram/) [neet code](https://youtu.be/9UtInBqnCgA)
