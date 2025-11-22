---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "Find Minimum Operations to Make All Elements Divisible by N"
date: "2025-11-22"
tags: Easy
categories:
  - "LeetCode Math"
---

- You are given an integer array `nums` and an integer `n`. In one operation, you can add or subtract 1 from **any** element of `nums`.
- Return the **minimum** number of operations to make all elements of `nums` divisible by `n`.

**Example 1**

```
Input: nums = [1,2,3,4], n = 3
Output: 3
Explanation:
All array elements can be made divisible by 3 using 3 operations:
Subtract 1 from 1.
Add 1 to 2.
Subtract 1 from 4.
```

**Example 2**

```
Input: nums = [3,6,9], n = 3
Output: 0
```

**Example 2**

```
Input: nums = [2,6,10,14], n = 4
Output: 8
Explanation:
All array elements can be made divisible by 4 using 8 operations:
Add 2 to 2.
Add 2 to 6.
Add 2 to 10.
Add 2 to 14.
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/11/22
 */
public class FindMinimumOperationsToMakeAllElementsDivisibleByN {

    public static int minimumOperations(int[] nums, int n) {
        int operations = 0; // Initialize the count of operations
        for (int num : nums) {
            int remainder = num % n; // Calculate the remainder when num is divided by n

            // If the number is already divisible by n, no operation is needed
            if (remainder == 0) {
                continue; // Skip to the next number
            }

            // Choose the operation (add or subtract) that requires the minimum steps
            operations += Math.min(remainder, n - remainder);
        }
        return operations; // Return the total count of operations
    }

    public static void main(String[] args) {
        // Test cases
        int[] nums1 = {1, 2, 3, 4};
        System.out.println("Divisible by 3: " + minimumOperations(nums1, 3)); // Output: 3

        int[] nums2 = {3, 6, 9};
        System.out.println("Divisible by 3: " + minimumOperations(nums2, 3)); // Output: 0

        int[] nums3 = {1, 5, 9, 13};
        System.out.println("Divisible by 4: " + minimumOperations(nums3, 4)); // Output: 4

        int[] nums4 = {2, 6, 10, 14};
        System.out.println("Divisible by 4: " + minimumOperations(nums4, 4)); // Output: 8
    }
}

```





