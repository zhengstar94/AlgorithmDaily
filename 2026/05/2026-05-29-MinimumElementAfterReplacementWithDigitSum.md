**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3300. Minimum Element After Replacement With Digit Sum"
date: "2026-05-29"
tags: Easy
categories:
  - "LeetCode Math"
---


- You are given an integer array `nums`.

- You replace each element in `nums` with the **sum** of its digits.

- Return the **minimum** element in `nums` after all replacements.



**Example 1**

```
Input: nums = [10,12,13,14]

Output: 1

Explanation:

nums becomes [1, 3, 4, 5] after all replacements, with minimum element 1.
```

**Example 2**

```
Input: nums = [1,2,3,4]

Output: 1

Explanation:

nums becomes [1, 2, 3, 4] after all replacements, with minimum element 1.
```

**Example 3**

```
Input: nums = [999,19,199]

Output: 10

Explanation:

nums becomes [27, 10, 19] after all replacements, with minimum element 10.
```

## Method 1

```tex
【O(nlogU) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2026/05/29
 */
public class MinimumElementAfterReplacementWithDigitSum {
    
    public static int minElement(int[] nums) {

        // Initialize answer with the largest possible integer value
        // so any computed result will be smaller
        int ans = Integer.MAX_VALUE;

        // Iterate through each number in the array
        for (int x : nums) {

            // Store the digit sum of current number
            int sum = 0;

            /**
             * Extract digits one by one using modulo and division:
             *
             * x % 10 -> gets the last digit
             * x / 10 -> removes the last digit
             *
             * Repeat until the number becomes 0
             */
            while (x > 0) {
                sum += x % 10; // add last digit to sum
                x /= 10;       // remove last digit
            }

            // Update the minimum value found so far
            ans = Math.min(ans, sum);
        }

        // Return the smallest digit sum
        return ans;
    }

    public static void main(String[] args) {

        // Test case 1:
        // 10 -> 1, 12 -> 3, 13 -> 4, 14 -> 5
        // minimum = 1
        int[] nums1 = {10, 12, 13, 14};
        System.out.println(minElement(nums1));

        // Test case 2:
        // Already single-digit numbers
        int[] nums2 = {1, 2, 3, 4};
        System.out.println(minElement(nums2));

        // Test case 3:
        // 999 -> 27, 19 -> 10, 199 -> 19
        // minimum = 10
        int[] nums3 = {999, 19, 199};
        System.out.println(minElement(nums3));
    }
}
```