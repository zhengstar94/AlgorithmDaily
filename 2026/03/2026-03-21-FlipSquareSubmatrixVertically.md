**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3643. Flip Square Submatrix Vertically"
date: "2026-03-21"
tags: Easy
categories:
  - "LeetCode Array"
---


- You are given an `m x n` integer matrix `grid`, and three integers `x`, `y`, and `k`.
- The integers `x` and `y` represent the row and column indices of the **top-left** corner of a **square** submatrix and the integer `k` represents the size (side length) of the square submatrix.
- Your task is to flip the submatrix by reversing the order of its rows vertically.
- Return the updated matrix.


**Example 1**

```
Input: grid = [[1,2,3,4],[5,6,7,8],[9,10,11,12],[13,14,15,16]], x = 1, y = 0, k = 3

Output: [[1,2,3,4],[13,14,15,8],[9,10,11,12],[5,6,7,16]]

Explanation:

The diagram above shows the grid before and after the transformation.
```

**Example 2**

```
Input: grid = [[3,4,2,3],[2,3,4,2]], x = 0, y = 2, k = 2

Output: [[3,4,4,2],[2,3,2,3]]

Explanation:

The diagram above shows the grid before and after the transformation.
```

## Method 1

```tex
【O(k^2) time | O(1) space】
```

```java
package Array;

import java.util.Arrays;

/**
 * @Author zhengxingxing
 * @Date 2026/03/21
 */
public class FlipSquareSubmatrixVertically {


    public static int[][] reverseSubmatrix(int[][] grid, int x, int y, int k) {
        // Initialize two pointers for the rows.
        // 'l' (left, or top) points to the first row of the submatrix.
        int l = x;
        // 'r' (right, or bottom) points to the last row of the submatrix.
        int r = x + k - 1;

        // Loop as long as the top pointer is above the bottom pointer.
        // This ensures we swap pairs of rows until they meet or cross in the middle.
        while (l < r) {
            // This inner loop iterates through each column within the submatrix's bounds.
            // The column range is from 'y' to 'y + k - 1'.
            for (int j = y; j < y + k; j++) {
                // Swap the elements at grid[l][j] and grid[r][j].
                // This is a standard in-place swap using a temporary variable.
                int tmp = grid[l][j];
                grid[l][j] = grid[r][j];
                grid[r][j] = tmp;
            }
            // After swapping a full row (within the submatrix columns),
            // move the top pointer down and the bottom pointer up to process the next pair of rows.
            l++;
            r--;
        }

        // Return the modified grid. In Java, arrays are passed by reference,
        // so the original grid object has been modified directly.
        return grid;
    }


    public static void main(String[] args) {
        // --- Test Case 1 ---
        System.out.println("--- Test Case 1 ---");
        int[][] grid1 = {
                {1, 2, 3, 4},
                {5, 6, 7, 8},
                {9, 10, 11, 12},
                {13, 14, 15, 16}
        };
        int x1 = 1, y1 = 0, k1 = 3;
        System.out.println("Original Grid:");
        printGrid(grid1);
        System.out.println("Parameters: x = " + x1 + ", y = " + y1 + ", k = " + k1);

        // Call the method to flip the submatrix.
        reverseSubmatrix(grid1, x1, y1, k1);

        System.out.println("\nGrid after flipping:");
        printGrid(grid1);

        int[][] expected1 = {{1, 2, 3, 4}, {13, 14, 15, 8}, {9, 10, 11, 12}, {5, 6, 7, 16}};
        System.out.println("\nExpected Output:");
        printGrid(expected1);
        System.out.println("--------------------\n");


        // --- Test Case 2 ---
        System.out.println("--- Test Case 2 ---");
        int[][] grid2 = {
                {3, 4, 2, 3},
                {2, 3, 4, 2}
        };
        int x2 = 0, y2 = 2, k2 = 2;
        System.out.println("Original Grid:");
        printGrid(grid2);
        System.out.println("Parameters: x = " + x2 + ", y = " + y2 + ", k = " + k2);

        // Call the method to flip the submatrix.
        reverseSubmatrix(grid2, x2, y2, k2);

        System.out.println("\nGrid after flipping:");
        printGrid(grid2);

        int[][] expected2 = {{3, 4, 4, 2}, {2, 3, 2, 3}};
        System.out.println("\nExpected Output:");
        printGrid(expected2);
        System.out.println("--------------------\n");
    }

    /**
     * Helper method to print a 2D array in a readable format.
     * @param grid The grid to be printed.
     */
    private static void printGrid(int[][] grid) {
        if (grid == null) {
            System.out.println("null");
            return;
        }
        for (int[] row : grid) {
            System.out.println(Arrays.toString(row));
        }
    }
}
```