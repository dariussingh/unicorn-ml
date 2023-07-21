---
layout: default
title: Contains Duplicate
parent: Arrays & Hashing
grand_parent: Data Structures and Algorithms
nav_order: 1
---

# Contains Duplicate

## Problem

Given an integer array `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: true
```

**Example 2:**

```
Input: nums = [1,2,3,4]
Output: false
```

**Example 3:**

```
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```

**Constraints:**

- `1 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`

## Solution

- HashMap
- Time: O(n)
- Space: O(n)

```python
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """

        hashset = set()

        for n in nums:
            if n in hashset:
                return True
            hashset.add(n)
        return False
```

## More Information

[leet code](https://leetcode.com/problems/contains-duplicate/) [neet code](https://youtu.be/3OamzN90kPg)
