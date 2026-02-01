---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3010. Divide an Array Into Subarrays With Minimum Cost I"
date: "2026-02-01"
tags: Easy
categories:
  - "LeetCode Greedy"
---


- You are given an array of integers `nums` of length `n`.
- The **cost** of an array is the value of its **first** element. For example, the cost of `[1,2,3]` is `1` while the cost of `[3,4,1]` is `3`.
- You need to divide `nums` into `3` **disjoint contiguous** subarrays.
- Return *the **minimum** possible **sum** of the cost of these subarrays*.

**Example 1**

```
Input: nums = [1,2,3,12]
Output: 6
Explanation: The best possible way to form 3 subarrays is: [1], [2], and [3,12] at a total cost of 1 + 2 + 3 = 6.
The other possible ways to form 3 subarrays are:
- [1], [2,3], and [12] at a total cost of 1 + 2 + 12 = 15.
- [1,2], [3], and [12] at a total cost of 1 + 3 + 12 = 16.
```

**Example 2**

```
Input: nums = [5,4,3]
Output: 12
Explanation: The best possible way to form 3 subarrays is: [5], [4], and [3] at a total cost of 5 + 4 + 3 = 12.
It can be shown that 12 is the minimum cost achievable.
```

**Example 3**

```
Input: nums = [10,3,1,1]
Output: 12
Explanation: The best possible way to form 3 subarrays is: [10,3], [1], and [1] at a total cost of 10 + 1 + 1 = 12.
It can be shown that 12 is the minimum cost achievable.
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Greedy;
import java.util.Arrays;

/**
 * @Author zhengxingxing
 * @Date 2026/02/01
 */
public class DivideAnArrayIntoSubarraysWithMinimumCostI {
    
    public static int minimumCost(int[] nums) {
        // The first element must always be the start of the first subarray
        int cost1 = nums[0];

        // Initialize variables to store the two smallest numbers found in the rest of the array
        int min1 = Integer.MAX_VALUE;
        int min2 = Integer.MAX_VALUE;

        // Iterate starting from the second element
        for (int i = 1; i < nums.length; i++) {
            int current = nums[i];

            // Update the smallest and second smallest values
            if (current < min1) {
                min2 = min1;
                min1 = current;
            } else if (current < min2) {
                min2 = current;
            }
        }

        // Return the sum of the first element and the two smallest subsequent elements
        return cost1 + min1 + min2;
    }

    public static void main(String[] args) {
        // Test Case 1
        int[] nums1 = {1, 2, 3, 12};
        System.out.println("Test Case 1: " + Arrays.toString(nums1));
        System.out.println("Output: " + minimumCost(nums1)); // Expected Output: 6
        System.out.println();

        // Test Case 2
        int[] nums2 = {5, 4, 3};
        System.out.println("Test Case 2: " + Arrays.toString(nums2));
        System.out.println("Output: " + minimumCost(nums2)); // Expected Output: 12
        System.out.println();

        // Test Case 3
        int[] nums3 = {10, 3, 1, 1};
        System.out.println("Test Case 3: " + Arrays.toString(nums3));
        System.out.println("Output: " + minimumCost(nums3)); // Expected Output: 12
        System.out.println();
    }
}
```