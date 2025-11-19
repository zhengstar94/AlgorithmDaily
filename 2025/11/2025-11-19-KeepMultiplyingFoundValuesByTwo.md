---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "2154. Keep Multiplying Found Values by Two"
date: "2025-11-19"
tags: Easy
categories:
  - "LeetCode Math"
---



- You are given an array of integers `nums`. You are also given an integer `original` which is the first number that needs to be searched for in `nums`.
- You then do the following steps:
  - If `original` is found in `nums`, **multiply** it by two (i.e., set `original = 2 * original`).
  - Otherwise, **stop** the process.
  - **Repeat** this process with the new number as long as you keep finding the number.
- Return *the **final** value of* `original`.


**Example 1**

```
Input: nums = [5,3,6,1,12], original = 3
Output: 24
Explanation: 
- 3 is found in nums. 3 is multiplied by 2 to obtain 6.
- 6 is found in nums. 6 is multiplied by 2 to obtain 12.
- 12 is found in nums. 12 is multiplied by 2 to obtain 24.
- 24 is not found in nums. Thus, 24 is returned.
```

**Example 2**

```
Input: nums = [2,7,9], original = 4
Output: 4
Explanation:
- 4 is not found in nums. Thus, 4 is returned.
```

## Method 1

```tex
【O(n) time | O(n) space】
```

```java
package Leetcode.Math;

import java.util.HashSet;
import java.util.Set;

/**
 * @Author zhengxingxing
 * @Date 2025/11/19
 */
public class KeepMultiplyingFoundValuesByTwo {
    public static int findFinalValue(int[] nums, int original) {
        // Use HashSet to store elements of nums for faster lookup
        Set<Integer> numSet = new HashSet<>();
        for (int num : nums) {
            numSet.add(num);
        }
        // Continuously search for original and multiply it by 2 until not found
        while (numSet.contains(original)) {
            original *= 2;
        }
        return original;
    }

    public static void main(String[] args) {
        // Test case 1
        int[] nums1 = {5, 3, 6, 1, 12};
        int original1 = 3;
        int result1 = findFinalValue(nums1, original1);
        System.out.println("Result of test case 1: " + result1); // Output: 24
        // Test case 2
        int[] nums2 = {2, 7, 9};
        int original2 = 4;
        int result2 = findFinalValue(nums2, original2);
        System.out.println("Result of test case 2: " + result2); // Output: 4
    }
}
```





