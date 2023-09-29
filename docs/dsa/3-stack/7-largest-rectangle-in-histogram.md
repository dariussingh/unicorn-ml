---
layout: default
title: Largest Rectangle In Histogram
parent: Stack
grand_parent: Data Structures and Algorithms
nav_order: 7
---

# Largest Rectangle In Histogram

## Problem

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return the area of the largest rectangle in the histogram.

**Example 1:**

![Example 1](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

```
Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.
```

**Example 2:**

![Example 2](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)

```
Input: heights = [2,4]
Output: 4
```

**Constraints:**

- `1 <= heights.length <= 105`
- `0 <= heights[i] <= 104`

## Solution

- Stack
- Time: O(n)
- Space: O(n)

```python
class Solution(object):
    def largestRectangleArea(self, heights):
        """
        :type heights: List[int]
        :rtype: int
        """
        maxArea = 0
        stack = [] # pairL (index, height)

        for i, h in enumerate(heights):
            start = i
            while stack and stack[-1][1] > h:
                index, height = stack.pop()
                maxArea = max(maxArea, height * (i - index))
                start = index
            stack.append((start, h))

        for i, h in stack:
            maxArea = max(maxArea, h * (len(heights) - i))
        return maxArea

```

## More Information

[leet code](https://leetcode.com/problems/largest-rectangle-in-histogram/) [neet code](https://youtu.be/zx5Sw9130L0?si=vnh2TXm1o4O6JjCn)
