---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "2348. Number of Zero-Filled Subarrays"
date: "2025-08-19"
tags: Medium
categories:
  - "LeetCode Math"
---


- Given an integer array `nums`, return *the number of **subarrays** filled with* `0`.
- A **subarray** is a contiguous non-empty sequence of elements within an array.

**Example 1**

```
Input: nums = [1,3,0,0,2,0,0,4]
Output: 6
Explanation: 
There are 4 occurrences of [0] as a subarray.
There are 2 occurrences of [0,0] as a subarray.
There is no occurrence of a subarray with a size more than 2 filled with 0. Therefore, we return 6.
```

**Example 2**

```
Input: nums = [0,0,0,2,0,0]
Output: 9
Explanation:
There are 5 occurrences of [0] as a subarray.
There are 3 occurrences of [0,0] as a subarray.
There is 1 occurrence of [0,0,0] as a subarray.
There is no occurrence of a subarray with a size more than 3 filled with 0. Therefore, we return 9.
```

**Example 3**

```
Input: nums = [2,10,2019]
Output: 0
Explanation: There is no subarray filled with 0. Therefore, we return 0.
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/08/19
 */
public class NumberOfZeroFilledSubarrays {

    public static long zeroFilledSubarray(int[] nums) {
        long result = 0;           // This variable stores the final count of zero-filled subarrays.
        int consecutiveZeros = 0;  // This variable counts the current streak of consecutive zeros.

        // Iterate through each element in the array.
        for (int num : nums) {
            if (num == 0) {
                // If the current element is 0, increment the count of consecutive zeros.
                consecutiveZeros++;
                // For each new zero in the streak, add the current streak length to the result.
                // This is because every new zero extends all previous zero-filled subarrays by one,
                // and also forms a new subarray by itself.
                result += consecutiveZeros;
            } else {
                // If the current element is not 0, reset the consecutive zero counter.
                consecutiveZeros = 0;
            }
        }

        // Return the total number of zero-filled subarrays found.
        return result;
    }

    public static void main(String[] args) {
        int[] nums1 = {1, 3, 0, 0, 2, 0, 0, 4};
        int[] nums2 = {0, 0, 0, 2, 0, 0};
        int[] nums3 = {2, 10, 2019};
        System.out.println(zeroFilledSubarray(nums1)); // Output: 6
        System.out.println(zeroFilledSubarray(nums2)); // Output: 9
        System.out.println(zeroFilledSubarray(nums3)); // Output: 0
    }
}

```





