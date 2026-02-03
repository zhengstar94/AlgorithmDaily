---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3637. Trionic Array I"
date: "2026-02-03"
tags: Easy
categories:
  - "LeetCode Greedy"
---


- You are given an integer array `nums` of length `n`.

- An array is **trionic** if there exist indices `0 < p < q < n − 1` such that:

  - `nums[0...p]` is **strictly** increasing,
  - `nums[p...q]` is **strictly** decreasing,
  - `nums[q...n − 1]` is **strictly** increasing.

- Return `true` if `nums` is trionic, otherwise return `false`.



**Example 1**

```
Input: nums = [1,3,5,4,2,6]
Output: true
Explanation:
Pick p = 2, q = 4:

nums[0...2] = [1, 3, 5] is strictly increasing (1 < 3 < 5).
nums[2...4] = [5, 4, 2] is strictly decreasing (5 > 4 > 2).
nums[4...5] = [2, 6] is strictly increasing (2 < 6).
```

**Example 2**

```
Input: nums = [2,1,3]
Output: false
Explanation:

There is no way to pick p and q to form the required three segments.
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Greedy;

/**
 * @Author zhengxingxing
 * @Date 2026/02/03
 */
public class TrionicArrayI {

    public static boolean isTrionic(int[] nums) {
        // Validate input: array must have at least 3 elements to form three segments
        if (nums == null || nums.length < 3) {
            return false;
        }

        // The first segment must be strictly increasing, otherwise return false immediately
        if (nums[0] >= nums[1]) {
            return false;
        }

        // stateChangeCount tracks the number of state transitions.
        // Initialized to 1 because we start in the increasing state.
        int stateChangeCount = 1;

        // Traverse from the 3rd element (index 2) to check trend changes in each consecutive triple
        for (int i = 2; i < nums.length; i++) {
            // Strictness check: equal elements are not allowed in a trionic array
            if (nums[i - 1] == nums[i]) {
                return false;
            }

            // Detects if the trend changes by comparing previous trend with current trend.
            // The XOR operation checks if one trend is increasing while the other is decreasing.
            // This identifies transition points between segments.
            if ((nums[i - 2] < nums[i - 1]) != (nums[i - 1] < nums[i])) {
                stateChangeCount++;

                // If state changes exceed 2 times (creating more than 3 segments),
                // the array cannot be trionic
                if (stateChangeCount > 3) {
                    return false;
                }
            }
        }

        // A valid trionic array must have exactly 3 states (which means 2 state changes)
        return stateChangeCount == 3;
    }

    /**
     * Main method for testing the isTrionic function with various test cases.
     */
    public static void main(String[] args) {
        // Test cases: each contains an array, expected result, and description
        Object[][] testData = {
                {new int[]{1, 3, 5, 4, 2, 6}, true, "Standard trionic array"},
                {new int[]{1, 2, 3, 2, 1, 0, 1, 2}, true, "Longer decreasing segment"},
        };

        System.out.println("Testing Trionic Array Algorithm:");
        for (int i = 0; i < testData.length; i++) {
            int[] nums = (int[]) testData[i][0];
            boolean expected = (Boolean) testData[i][1];
            String desc = (String) testData[i][2];

            boolean result = isTrionic(nums);
            String status = (result == expected) ? "✓ Pass" : "✗ Fail";

            System.out.printf("%d. %s: %s %s %s\n",
                    i + 1, desc, result, status, java.util.Arrays.toString(nums));
        }
    }
}

```