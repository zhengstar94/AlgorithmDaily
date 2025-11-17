---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1437. Check If All 1's Are at Least Length K Places Away"
date: "2025-11-17"
tags: Easy
categories:
  - "LeetCode Math"
---


- Given an binary array `nums` and an integer `k`, return `true` *if all* `1`*'s are at least* `k` *places away from each other, otherwise return* `false`.

**Example 1**

```
Input: nums = [1,0,0,0,1,0,0,1], k = 2
Output: true
Explanation: Each of the 1s are at least 2 places away from each other.
```

**Example 2**

```
Input: nums = [1,0,0,1,0,1], k = 2
Output: false
Explanation: The second 1 and third 1 are only one apart from each other.
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/11/17
 */
public class CheckIfAll1sAreAtLeastLengthKPlacesAway {

    public static boolean kLengthApart(int[] nums, int k) {
        int lastOne = -1; // Record the position of the last occurrence of 1, initialized to -1
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 1) {
                if (lastOne != -1 && i - lastOne <= k) {
                    return false; // If the distance between the current 1 and the last 1 is less than or equal to k, return false
                }
                lastOne = i; // Update the position of the last 1
            }
        }
        return true; // If traversing the array does not find any 1s with a distance less than k, return true
    }

    public static void main(String[] args) {
        // Test cases
        int[] nums1 = {1, 0, 0, 0, 1, 0, 0, 1};
        int k1 = 2;
        System.out.println("Test Case 1: " + kLengthApart(nums1, k1)); // Output: true
        int[] nums2 = {1, 0, 0, 1, 0, 1};
        int k2 = 2;
        System.out.println("Test Case 2: " + kLengthApart(nums2, k2)); // Output: false
    }
}

```





