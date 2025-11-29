---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3512. Minimum Operations to Make Array Sum Divisible by K"
date: "2025-11-29"
tags: Easy
categories:
  - "LeetCode Math"
---


- You are given an integer array `nums` and an integer `k`. You can perform the following operation any number of times:
  - Select an index `i` and replace `nums[i]` with `nums[i] - 1`.
- Return the **minimum** number of operations required to make the sum of the array divisible by `k`.

**Example 1**

```
Input: nums = [3,9,7], k = 5
Output: 4

Explanation:
Perform 4 operations on nums[1] = 9. Now, nums = [3, 5, 7].
The sum is 15, which is divisible by 5.
```

**Example 2**

```
Input: nums = [4,1,3], k = 4
Output: 0

Explanation:
The sum is 8, which is already divisible by 4. Hence, no operations are needed.

```

**Example 3**

```
Input: nums = [3,2], k = 6
Output: 5

Explanation:
Perform 3 operations on nums[0] = 3 and 2 operations on nums[1] = 2. Now, nums = [0, 0].
The sum is 0, which is divisible by 6.
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/11/29
 */
public class MinimumOperationsToMakeArraySumDivisibleByK {

    public static int minOperations(int[] nums, int k) {
        int s = 0; // Initialize the sum of the array elements
        for (int x : nums) {
            s += x; // Calculate the sum of all elements in the array
        }
        return s % k; // Return the remainder when the sum is divided by k, which represents the minimum operations
    }

    public static void main(String[] args) {
        // Test case 1
        int[] nums1 = {3, 9, 7};
        int k1 = 5;
        int result1 = minOperations(nums1, k1);
        System.out.println("Result of test case 1: " + result1); // Output: 4
        // Test case 2
        int[] nums2 = {4, 1, 3};
        int k2 = 4;
        int result2 = minOperations(nums2, k2);
        System.out.println("Result of test case 2: " + result2); // Output: 0
        // Test case 3
        int[] nums3 = {3, 2};
        int k3 = 6;
        int result3 = minOperations(nums3, k3);
        System.out.println("Result of test case 3: " + result3); // Output: 5
    }
}
```





