**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "2574. Left and Right Sum Differences"
date: "2026-06-06"
tags: Easy
categories:
  - "LeetCode Array"
---


- You are given a **0-indexed** integer array `nums` of size `n`.

- Define two arrays `leftSum` and `rightSum` where:

  - `leftSum[i]` is the sum of elements to the left of the index `i` in the array `nums`. If there is no such element, `leftSum[i] = 0`.
  - `rightSum[i]` is the sum of elements to the right of the index `i` in the array `nums`. If there is no such element, `rightSum[i] = 0`.

- Return an integer array `answer` of size `n` where `answer[i] = |leftSum[i] - rightSum[i]|`.



**Example 1**

```
Input: nums = [10,4,8,3]
Output: [15,1,11,22]
Explanation: The array leftSum is [0,10,14,22] and the array rightSum is [15,11,3,0].
The array answer is [|0 - 15|,|10 - 11|,|14 - 3|,|22 - 0|] = [15,1,11,22].
```

**Example 2**

```
Input: nums = [1]
Output: [0]
Explanation: The array leftSum is [0] and the array rightSum is [0].
The array answer is [|0 - 0|] = [0].
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Array;

import java.util.Arrays;

/**
 * Author: zhengxingxing
 * Date: 2026/06/06
 */
public class LeftAndRightSumDifferences {
    
    public static int[] leftRigthDifference(int[] nums) {

        // Calculate the sum of all elements in the array.
        int total = 0;
        for (int x : nums) {
            total += x;
        }

        // Running prefix sum representing the sum of elements
        // to the left of the current index.
        int leftSum = 0;

        for (int i = 0; i < nums.length; i++) {

            // Save the original value because nums[i]
            // will be overwritten by the result.
            int x = nums[i];

            // Compute:
            // |leftSum - rightSum|
            //
            // Using the derived formula:
            // |2 * leftSum + x - total|
            nums[i] = Math.abs(2 * leftSum + x - total);

            // Update prefix sum for the next iteration.
            leftSum += x;
        }

        return nums;
    }

    public static void main(String[] args) {

        int[] nums1 = {10, 4, 8, 3};
        System.out.println(Arrays.toString(leftRigthDifference(nums1)));
        // Expected output: [15, 1, 11, 22]

        int[] nums2 = {1};
        System.out.println(Arrays.toString(leftRigthDifference(nums2)));
        // Expected output: [0]
    }
}
```