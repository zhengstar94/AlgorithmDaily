---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3000. Maximum Area of Longest Diagonal Rectangle"
date: "2025-08-26"
tags: Medium
categories:
  - "LeetCode Array"
---

- You are given a 2D **0-indexed** integer array `dimensions`.
- For all indices `i`, `0 <= i < dimensions.length`, `dimensions[i][0]` represents the length and `dimensions[i][1]` represents the width of the rectangle `i`.
- Return *the **area** of the rectangle having the **longest** diagonal. If there are multiple rectangles with the longest diagonal, return the area of the rectangle having the **maximum** area.*

**Example 1**

```
Input: dimensions = [ [ 9,3],[8,6 ] ]
Output: 48
Explanation: 
For index = 0, length = 9 and width = 3. Diagonal length = sqrt(9 * 9 + 3 * 3) = sqrt(90) ≈ 9.487.
For index = 1, length = 8 and width = 6. Diagonal length = sqrt(8 * 8 + 6 * 6) = sqrt(100) = 10.
So, the rectangle at index 1 has a greater diagonal length therefore we return area = 8 * 6 = 48.
```

**Example 2**

```
Input: dimensions = [ [3,4],[4,3] ]
Output: 12
Explanation: Length of diagonal is the same for both which is 5, so maximum area = 12.
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Array;

/**
 * @Author zhengxingxing
 * @Date 2025/08/26
 */
public class MaximumAreaOfLongestDiagonalRectangle {

    public static int areaOfMaxDiagonal(int[][] dimensions) {
        int ans = 0;   // Stores the maximum area found so far
        int maxL = 0;  // Stores the maximum diagonal squared found so far

        // Iterate through each rectangle in the input array
        for (int[] d : dimensions) {
            int x = d[0], y = d[1];           // x: length, y: width
            int l = x * x + y * y;            // Calculate the square of the diagonal (no need for sqrt)

            // If this rectangle has a longer diagonal, or
            // if the diagonal is the same but the area is larger, update the answer
            if (l > maxL || (l == maxL && x * y > ans)) {
                maxL = l;                     // Update the maximum diagonal squared
                ans = x * y;                  // Update the maximum area
            }
        }
        return ans; // Return the area of the rectangle with the longest diagonal (and largest area if tie)
    }

    public static void main(String[] args) {
        // Test case 1: The rectangle [8, 6] has the longest diagonal (10), area = 48
        int[][] test1 = { {9, 3}, {8, 6} };
        // Test case 2: Both rectangles have the same diagonal (5), max area = 12
        int[][] test2 = { {3, 4}, {4, 3} };
        // Test case 3: [13, 5] has the longest diagonal (sqrt(194)), area = 65
        int[][] test3 = { {5, 12}, {13, 5}, {6, 8} };

        System.out.println(areaOfMaxDiagonal(test1)); // Output: 48
        System.out.println(areaOfMaxDiagonal(test2)); // Output: 12
        System.out.println(areaOfMaxDiagonal(test3)); // Output: 65
    }
}

```





