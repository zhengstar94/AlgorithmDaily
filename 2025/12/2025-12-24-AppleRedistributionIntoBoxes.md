---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3074. Apple Redistribution into Boxes"
date: "2025-12-24"
tags: Easy
categories:
  - "LeetCode Greedy"
---

- You are given an array `apple` of size `n` and an array `capacity` of size `m`.

- There are `n` packs where the `ith` pack contains `apple[i]` apples. There are `m` boxes as well, and the `ith` box has a capacity of `capacity[i]` apples.

- Return *the **minimum** number of boxes you need to select to redistribute these* `n` *packs of apples into boxes*.

  **Note** that, apples from the same pack can be distributed into different boxes.

**Example 1**

```
Input: apple = [1,3,2], capacity = [4,3,1,5,2]
Output: 2
Explanation: We will use boxes with capacities 4 and 5.
It is possible to distribute the apples as the total capacity is greater than or equal to the total number of apples.
```

**Example 2**

```
Input: apple = [5,5,5], capacity = [2,4,2,7]
Output: 4
Explanation: We will need to use all the boxes.
```

## Method 1

```tex
【O(m * logm) time | O(1) space】
```

```java
package Leetcode.Greedy;

import java.util.Arrays;

/**
 * @Author zhengxingxing
 * @Date 2025/12/24
 */
public class AppleRedistributionIntoBoxes {
    
    public static int minimumBoxes(int[] apple, int[] capacity) {
        // 1. Calculate the total number of apples
        int totalApples = 0;
        for (int numApples : apple) {
            totalApples += numApples;
        }

        // 2. Sort the box capacities in ascending order to easily use boxes from largest to smallest
        Arrays.sort(capacity);

        // 3. Iterate through the boxes starting from the largest capacity, until all apples are distributed
        int numBoxes = 0; // Counter for the number of boxes used
        int boxIndex = capacity.length - 1;  // Start from the last box (largest capacity)

        while (totalApples > 0 && boxIndex >= 0) {
            totalApples -= capacity[boxIndex]; // Use a box: subtract box capacity from the remaining apples
            numBoxes++;                      // Increment the number of boxes used
            boxIndex--;                      // Move to the next box (smaller capacity)
        }

        // 4. Return the total number of boxes used
        return numBoxes;
    }

    public static void main(String[] args) {
        // Test case 1
        int[] apple1 = {1, 3, 2};
        int[] capacity1 = {4, 3, 1, 5, 2};
        System.out.println("Example 1: " + minimumBoxes(apple1, capacity1)); // Output: 2

        // Test case 2
        int[] apple2 = {5, 5, 5};
        int[] capacity2 = {2, 4, 2, 7};
        System.out.println("Example 2: " + minimumBoxes(apple2, capacity2)); // Output: 4
    }
}

```





