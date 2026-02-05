---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3379. Transformed Array"
date: "2026-02-05"
tags: Easy
categories:
  - "LeetCode Array"
---


- You are given an integer array `nums` that represents a circular array. Your task is to create a new array `result` of the **same** size, following these rules:
- For each index `i` (where `0 <= i < nums.length`), perform the following **independent** actions:
  - If `nums[i] > 0`: Start at index `i` and move `nums[i]` steps to the **right** in the circular array. Set `result[i]` to the value of the index where you land.
  - If `nums[i] < 0`: Start at index `i` and move `abs(nums[i])` steps to the **left** in the circular array. Set `result[i]` to the value of the index where you land.
  - If `nums[i] == 0`: Set `result[i]` to `nums[i]`.
- Return the new array `result`.
- **Note:** Since `nums` is circular, moving past the last element wraps around to the beginning, and moving before the first element wraps back to the end.

**Example 1**

```
Input: nums = [3,-2,1,1]

Output: [1,1,1,3]

Explanation:

For nums[0] that is equal to 3, If we move 3 steps to right, we reach nums[3]. So result[0] should be 1.
For nums[1] that is equal to -2, If we move 2 steps to left, we reach nums[3]. So result[1] should be 1.
For nums[2] that is equal to 1, If we move 1 step to right, we reach nums[3]. So result[2] should be 1.
For nums[3] that is equal to 1, If we move 1 step to right, we reach nums[0]. So result[3] should be 3.
```

**Example 2**

```
Input: nums = [-1,4,-1]

Output: [-1,-1,4]

Explanation:

For nums[0] that is equal to -1, If we move 1 step to left, we reach nums[2]. So result[0] should be -1.
For nums[1] that is equal to 4, If we move 4 steps to right, we reach nums[2]. So result[1] should be -1.
For nums[2] that is equal to -1, If we move 1 step to left, we reach nums[1]. So result[2] should be 4.
```

## Method 1

```tex
【O(n) time | O(n) space】
```

```java
package Leetcode.Array;

import java.util.Arrays;

/**
 * @Author zhengxingxing
 * @Date 2026/02/05
 */
public class TransformedArray {
    public static int[] constructTransformedArray(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];

        for (int i = 0; i < n; i++) {
            // Step 1: Calculate effective steps in circular array
            // The % n operation handles the circular nature: moving n steps brings you back to start
            // This gives us steps in range [-(n-1), n-1]
            int step = nums[i] % n;

            // Step 2: Convert negative steps (left moves) to equivalent positive steps (right moves)
            // KEY EXPLANATION: 
            // - When step is negative, it means we need to move LEFT by |step| positions
            // - In a circular array, moving LEFT by k steps is EQUIVALENT to moving RIGHT by (n - k) steps
            // - Since step is negative, step = -k for some positive k
            // - Adding n to step: step + n = -k + n = n - k, which is the equivalent RIGHTWARD steps
            // Example: n=5, step=-3 (move left 3)
            //   step += n → -3 + 5 = 2 (equivalent to moving right 2)
            if (step < 0){
                step += n;
            }

            // Step 3: Calculate the target index after moving RIGHT by 'step' positions
            // The % n handles wrap-around: if (i + step) exceeds array bounds, it wraps to beginning
            int target = (i + step) % n;

            // Step 4: Assign the value at target index to result[i]
            result[i] = nums[target];
        }

        return result;
    }

    public static void main(String[] args) {
        int[][] testCases = {
                {3, -2, 1, 1},      // Example 1
                {-1, 4, -1},        // Example 2
                {0, 0, 0},          // All zeros
                {5, -5, 10, -10},   // Steps larger than n
                {1},                // Single element
                {2, 2, 2},          // Uniform positive numbers
        };
        for (int[] tc : testCases) {
            System.out.println(Arrays.toString(tc) + " → "
                    + Arrays.toString(constructTransformedArray(tc)));
        }
    }
}

```