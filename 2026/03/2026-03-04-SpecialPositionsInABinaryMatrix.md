**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1582. Special Positions in a Binary Matrix"
date: "2026-03-04"
tags: Easy
categories:
  - "LeetCode Array"
---


- Given an `m x n` binary matrix `mat`, return *the number of special positions in* `mat`*.*
- A position `(i, j)` is called **special** if `mat[i][j] == 1` and all other elements in row `i` and column `j` are `0` (rows and columns are **0-indexed**).


**Example 1**

```
Input: mat = [[1,0,0],[0,0,1],[1,0,0]]
Output: 1
Explanation: (1, 2) is a special position because mat[1][2] == 1 and all other elements in row 1 and column 2 are 0.
```

**Example 2**

```
Input: mat = [[1,0,0],[0,1,0],[0,0,1]]
Output: 3
Explanation: (0, 0), (1, 1) and (2, 2) are special positions.
```

## Method 1

```tex
【O(mn) time | O(1) space】
```

```java
package Array;

/**
 * @author zhengstars
 * @date 2026/03/04
 */
public class SpecialPositionsInABinaryMatrix {

    public static int numSpecial(int[][] mat) {

        // Number of rows
        int m = mat.length;

        // Number of columns
        int n = mat[0].length;

        // row[i] stores how many 1s are in row i
        int[] row = new int[m];

        // col[j] stores how many 1s are in column j
        int[] col = new int[n];

        // First traversal: count 1s for each row and column
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (mat[i][j] == 1) {
                    row[i]++;
                    col[j]++;
                }
            }
        }

        int count = 0;

        // Second traversal: check special positions
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                // A position is special if:
                // 1. The value is 1
                // 2. The row contains exactly one 1
                // 3. The column contains exactly one 1
                if (mat[i][j] == 1 && row[i] == 1 && col[j] == 1) {
                    count++;
                }
            }
        }

        return count;
    }

    public static void main(String[] args) {

        int[][] mat1 = {
                {1, 0, 0},
                {0, 0, 1},
                {1, 0, 0}
        };

        int[][] mat2 = {
                {1, 0, 0},
                {0, 1, 0},
                {0, 0, 1}
        };

        System.out.println("Example 1 Output: " + numSpecial(mat1)); // Expected: 1
        System.out.println("Example 2 Output: " + numSpecial(mat2)); // Expected: 3
    }
}
```