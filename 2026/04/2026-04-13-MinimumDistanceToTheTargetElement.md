**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1848. Minimum Distance to the Target Element"
date: "2026-04-13"
tags: Easy
categories:
  - "LeetCode Array"
---

- Given an integer array `nums` **(0-indexed)** and two integers `target` and `start`, find an index `i` such that `nums[i] == target` and `abs(i - start)` is **minimized**. Note that `abs(x)` is the absolute value of `x`.
- Return `abs(i - start)`.
- It is **guaranteed** that `target` exists in `nums`.

**Example 1**

```
Input: nums = [1,2,3,4,5], target = 5, start = 3
Output: 1
Explanation: nums[4] = 5 is the only value equal to target, so the answer is abs(4 - 3) = 1.
```

**Example 2**

```
Input: nums = [1], target = 1, start = 0
Output: 0
Explanation: nums[0] = 1 is the only value equal to target, so the answer is abs(0 - 0) = 0.
```

**Example 3**

```
Input: nums = [1,1,1,1,1,1,1,1,1,1], target = 1, start = 0
Output: 0
Explanation: Every value of nums is 1, but nums[0] minimizes abs(i - start), which is abs(0 - 0) = 0.
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Array;

/**
 * @Author zhengxingxing
 * @Date 2026/04/13
 */
public class MinimumDistanceToTheTargetElement {
    
    public static int getMinDistance(int[] nums, int target, int start) {
        int ans = nums.length;

        // Traverse the array and check every element
        for (int i = 0; i < nums.length; i++) {

            // If the current element equals the target,
            // compute the distance from the current index to start
            if (nums[i] == target) {
                ans = Math.min(ans, Math.abs(i - start));
            }
        }

        // Return the smallest distance found
        return ans;
    }

    public static void main(String[] args) {
        // Test case 1:
        // The target value 5 appears at index 4.
        // Distance = |4 - 3| = 1
        int[] nums1 = {1, 2, 3, 4, 5};
        int target1 = 5;
        int start1 = 3;
        System.out.println("Test case 1 result: " + getMinDistance(nums1, target1, start1));
        System.out.println("Expected result: 1");
        System.out.println();

        // Test case 2:
        // The array contains only one element, which is also the target.
        // Distance = |0 - 0| = 0
        int[] nums2 = {1};
        int target2 = 1;
        int start2 = 0;
        System.out.println("Test case 2 result: " + getMinDistance(nums2, target2, start2));
        System.out.println("Expected result: 0");
        System.out.println();

        // Test case 3:
        // Every element is the target value.
        // The closest target to start index 0 is index 0 itself.
        // Distance = |0 - 0| = 0
        int[] nums3 = {1, 1, 1, 1, 1, 1, 1, 1, 1, 1};
        int target3 = 1;
        int start3 = 0;
        System.out.println("Test case 3 result: " + getMinDistance(nums3, target3, start3));
        System.out.println("Expected result: 0");
        System.out.println();
    }
}
```