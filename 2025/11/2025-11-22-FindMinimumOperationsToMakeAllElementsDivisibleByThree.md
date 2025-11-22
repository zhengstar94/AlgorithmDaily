---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3190. Find Minimum Operations to Make All Elements Divisible by Three"
date: "2025-11-22"
tags: Easy
categories:
  - "LeetCode Math"
---



- You are given an integer array `nums`. In one operation, you can add or subtract 1 from **any** element of `nums`.
- Return the **minimum** number of operations to make all elements of `nums` divisible by 3.


**Example 1**

```
Input: nums = [1,2,3,4]
Output: 3

Explanation:
All array elements can be made divisible by 3 using 3 operations:
Subtract 1 from 1.
Add 1 to 2.
Subtract 1 from 4.
```

**Example 2**

```
Input: nums = [3,6,9]
Output: 0
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
public class FindMinimumOperationsToMakeAllElementsDivisibleByThree {

    public static int minimumOperations(int[] nums) {
        int count = 0; // Initialize the count of operations
        for (int num : nums) {
            if (num % 3 == 0) { // If the number is already divisible by 3
                continue;       // Skip to the next number
            }
            count++;            // Increment the count if the number is not divisible by 3
        }
        return count;           // Return the total count of operations
    }

    public static void main(String[] args) {
        // Test cases
        int[] nums1 = {1, 2, 3, 4};
        System.out.println(minimumOperations(nums1)); // Output: 3
        int[] nums2 = {3, 6, 9};
        System.out.println(minimumOperations(nums2)); // Output: 0
    }
}

```





