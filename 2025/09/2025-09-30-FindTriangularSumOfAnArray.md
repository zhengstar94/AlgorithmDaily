---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "2221. Find Triangular Sum of an Array"
date: "2025-09-28"
tags: Medium
categories:
  - "LeetCode Math"
---


- You are given a **0-indexed** integer array `nums`, where `nums[i]` is a digit between `0` and `9` (**inclusive**).
- The **triangular sum** of `nums` is the value of the only element present in `nums` after the following process terminates:
  - Let `nums` comprise of `n` elements. If `n == 1`, **end** the process. Otherwise, **create** a new **0-indexed** integer array `newNums` of length `n - 1`.
  - For each index `i`, where `0 <= i < n - 1`, **assign** the value of `newNums[i]` as `(nums[i] + nums[i+1]) % 10`, where `%` denotes modulo operator.
  - **Replace** the array `nums` with `newNums`.
  - **Repeat** the entire process starting from step 1.
- Return *the triangular sum of* `nums`.

**Example 1**

```
Input: nums = [1,2,3,4,5]
Output: 8
Explanation:
The above diagram depicts the process from which we obtain the triangular sum of the array.
```

**Example 2**

```
Input: nums = [5]
Output: 5
Explanation:
Since there is only one element in nums, the triangular sum is the value of that element itself.
```

## Method 1

```tex
【O(n^2) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/09/30
 */
public class FindTriangularSumOfAnArray {

    public static int triangularSum(int[] nums) {
        // Iterate until the array is reduced to a single element
        for (int n = nums.length - 1; n > 0; n--) {
            // Calculate the new value for each element based on the sum of adjacent elements modulo 10
            for (int i = 0; i < n; i++) {
                nums[i] = (nums[i] + nums[i + 1]) % 10;
            }
        }
        // The remaining element in the array is the triangular sum
        return nums[0];
    }

    public static void main(String[] args) {
        // Test case 1
        int[] nums1 = {1, 2, 3, 4, 5};
        int result1 = triangularSum(nums1);
        System.out.println("Triangular Sum (Example 1): " + result1);  // Output: 8

        // Test case 2
        int[] nums2 = {5};
        int result2 = triangularSum(nums2);
        System.out.println("Triangular Sum (Example 2): " + result2);  // Output: 5
    }
}

```





