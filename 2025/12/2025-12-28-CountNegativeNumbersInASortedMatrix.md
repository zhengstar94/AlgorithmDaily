---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1351. Count Negative Numbers in a Sorted Matrix"
date: "2025-12-28"
tags: Easy
categories:
  - "LeetCode Array"
---


- Given a `m x n` matrix `grid` which is sorted in non-increasing order both row-wise and column-wise, return *the number of **negative** numbers in* `grid`.

**Example 1**

```
Input: grid = [[4,3,2,-1],[3,2,1,-1],[1,1,-1,-2],[-1,-1,-2,-3]]
Output: 8
Explanation: There are 8 negatives number in the matrix.
```

**Example 2**

```
Input: grid = [[3,2],[1,0]]
Output: 0
```

## Method 1

```tex
【O(m + n) time | O(1) space】
```

```java
package Leetcode.Array;

/**
 * @Author zhengxingxing
 * @Date 2025/12/28
 */
public class CountNegativeNumbersInASortedMatrix {


    public static int countNegatives(int[][] grid) {
        int m = grid.length; // Number of rows in the matrix
        int n = grid[0].length; // Number of columns in the matrix
        int row = 0; // Start from the first row (index 0)
        int col = n - 1; // Start from the last column (rightmost column)
        int count = 0; // Initialize the count of negative numbers

        // Iterate while the row index is within bounds and the column index is non-negative
        while (row < m && col >= 0) {
            if (grid[row][col] < 0) {
                // Current element is negative, implying all elements in the current column
                // below the current row are also negative due to the sorted property.
                count += m - row; // Increment count by the number of negative elements (rows below)
                col--; // Move to the left column (towards smaller elements)
            } else {
                // Current element is non-negative, implying all elements in the current row
                // to the left of the current column are also non-negative due to the sorted property.
                row++; // Move to the next row (towards smaller elements)
            }
        }

        return count; // Return the total number of negative numbers found
    }

    public static void main(String[] args) {
        // Test case 1
        int[][] grid1 = {{4, 3, 2, -1}, {3, 2, 1, -1}, {1, 1, -1, -2}, {-1, -1, -2, -3}};
        int result1 = countNegatives(grid1);
        System.out.println("Test Case 1: " + result1);  // Output: 8

        // Test case 2
        int[][] grid2 = {{3, 2}, {1, 0}};
        int result2 = countNegatives(grid2);
        System.out.println("Test Case 2: " + result2);  // Output: 0
    }
}

```





