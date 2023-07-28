---
layout: default
title: Longest Consecutive Sequence
parent: Arrays & Hashing
grand_parent: Data Structures and Algorithms
nav_order: 8
---

# Longest Consecutive Sequence

## Problem

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in `O(n)` time.

**Example 1:**

```
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

**Example 2:**

```
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

Constraints:

- `0 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`

## Solution

- Array
- Time: O(n)
- Space: O(n)

```python
class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        numSet = set(nums)
        longest = 0

        for n in nums:
            if (n - 1) not in numSet:
                length = 0

                while (n + length) in numSet:
                    length += 1
                longest = max(length, longest)

        return longest
```

## More Information

[leet code](https://leetcode.com/problems/longest-consecutive-sequence/) [neet code](https://youtu.be/P6RZZMu_maU)
