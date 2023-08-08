---
layout: default
title: Container With Most Water
parent: Two Pointers
grand_parent: Data Structures and Algorithms
nav_order: 4
---

# Container With Most Water

## Problem

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

**Example 1:**

![Example 1](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are
represented by array [1,8,6,2,5,4,8,3,7].
In this case, the max area of water (blue
section) the container can contain is 49.
```

**Example 2:**

```
Input: height = [1,1]
Output: 1
```

**Constraints:**

- `n == height.length`
- `2 <= n <= 105`
- `0 <= height[i] <= 104`

## Solution

- Two Pointers
- Time: O(n)
- Space: O(1)

```python
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        result = 0

        l = 0
        r = len(height) - 1

        while l < r:
            area = (r - l) * min(height[r], height[l])

            if area > result:
                result = area

            if height[l] < height[r]:
                l += 1
            else:
                r -= 1

        return result
```

## More Information

[leet code](https://leetcode.com/problems/container-with-most-water/) [neet code](https://youtu.be/UuiTKBwPgAo)
