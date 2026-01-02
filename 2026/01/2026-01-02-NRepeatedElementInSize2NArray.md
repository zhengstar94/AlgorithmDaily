---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "961. N-Repeated Element in Size 2N Array"
date: "2026-01-02"
tags: Easy
categories:
  - "LeetCode Array"
---



- You are given an integer array `nums` with the following properties:
  - `nums.length == 2 * n`.
  - `nums` contains `n + 1` **unique** elements.
  - Exactly one element of `nums` is repeated `n` times.
- Return *the element that is repeated* `n` *times*.


**Example 1**

```
Input: nums = [1,2,3,3]
Output: 3
```

**Example 2**

```
Input: nums = [2,1,2,5,3,2]
Output: 2
```

**Example 2**

```
Input: nums = [5,1,5,2,5,3,5,4]
Output: 5
```

## Method 1

```tex
【O(m + n) time | O(1) space】
```

```java
package Leetcode.Array;

import java.util.HashSet;

/**
 * @Author zhengxingxing
 * @Date 2026/01/02
 */
public class NRepeatedElementInSize2NArray {
    
    public static int repeatedNTimes(int[] nums) {
        HashSet<Integer> seen = new HashSet<>();

        for (int x : nums) {
            if (!seen.add(x)) {
                return x;
            }
        }

        return -1; // Should not happen as per problem constraints
    }

    public static void main(String[] args) {
        // Test cases
        int[] nums1 = {1, 2, 3, 3};
        System.out.println("Array: " + java.util.Arrays.toString(nums1) + ", Repeated Element: " + repeatedNTimes(nums1)); // Output: 3
        int[] nums2 = {2, 1, 2, 5, 3, 2};
        System.out.println("Array: " + java.util.Arrays.toString(nums2) + ", Repeated Element: " + repeatedNTimes(nums2)); // Output: 2
        int[] nums3 = {5, 1, 5, 2, 5, 3, 5, 4};
        System.out.println("Array: " + java.util.Arrays.toString(nums3) + ", Repeated Element: " + repeatedNTimes(nums3)); // Output: 5
    }
}

```





