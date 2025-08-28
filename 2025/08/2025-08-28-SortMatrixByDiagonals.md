---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3446. Sort Matrix by Diagonals"
date: "2025-08-28"
tags: Medium
categories:
  - "LeetCode HashTable"
---


- You are given an `n x n` square matrix of integers `grid`. Return the matrix such that:
  - The diagonals in the **bottom-left triangle** (including the middle diagonal) are sorted in **non-increasing order**.
  - The diagonals in the **top-right triangle** are sorted in **non-decreasing order**.

**Example 1**

```
Input: grid = [[1,7,3],[9,8,2],[4,5,6]]
Output: [[8,2,3],[9,6,7],[4,5,1]]

The diagonals with a black arrow (bottom-left triangle) should be sorted in non-increasing order:

[1, 8, 6] becomes [8, 6, 1].
[9, 5] and [4] remain unchanged.
The diagonals with a blue arrow (top-right triangle) should be sorted in non-decreasing order:

[7, 2] becomes [2, 7].
[3] remains unchanged.
```

**Example 2**

```
Input: grid = [[0,1],[1,2]]
Output: [[2,1],[1,0]]
The diagonals with a black arrow must be non-increasing, so [0, 2] is changed to [2, 0]. The other diagonals are already in the correct order.
```

**Example 3**

```
Input: grid = [[1]]
Output: [[1]]
Explanation:
Diagonals with exactly one element are already in order, so no changes are needed.
```

## Method 1

```tex
【O(n^2*log(n)) time | O(n^2) space】
```

```java
package Leetcode.HashTable;

import java.util.*;

/**
 * @Author zhengxingxing
 * @Date 2025/08/28
 */
public class SortMatrixByDiagonals {
    public static int[][] sortMatrixByDiagonals(int[][] grid) {
        int n = grid.length;

        // Step 1: Group all elements by their diagonal index (i - j).
        // The key is (i - j), which uniquely identifies each diagonal in the matrix.
        // The value is a list of all elements on that diagonal.
        Map<Integer, List<Integer>> diagMap = new HashMap<>();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                int key = i - j; // Calculate the diagonal index for the current element.
                // If the diagonal does not exist in the map, create a new list for it.
                // Then, add the current element to the corresponding diagonal list.
                diagMap.computeIfAbsent(key, k -> new ArrayList<>()).add(grid[i][j]);
            }
        }

        // Step 2: Sort each diagonal according to the problem's requirements.
        // For diagonals in the bottom-left triangle (including the main diagonal, key >= 0),
        // sort in non-increasing (descending) order.
        // For diagonals in the top-right triangle (key < 0), sort in non-decreasing (ascending) order.
        for (int key: diagMap.keySet()) {
            List<Integer> diag = diagMap.get(key);
            if (key >= 0){
                // Descending order for bottom-left triangle and main diagonal
                diag.sort(Collections.reverseOrder());
            } else {
                // Ascending order for top-right triangle
                Collections.sort(diag);
            }
        }

        // Step 3: Fill the sorted values back into a new result matrix.
        // We need to keep track of how many elements have been used from each diagonal.
        // diagIndex maps each diagonal key to the next index to use in its sorted list.
        Map<Integer, Integer> diagIndex = new HashMap<>();
        int[][] res = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                int key = i - j; // Find the diagonal for the current position.
                // Get the current index for this diagonal, defaulting to 0 if not present.
                int idx = diagIndex.getOrDefault(key, 0);
                // Place the next sorted value from the diagonal into the result matrix.
                res[i][j] = diagMap.get(key).get(idx);
                // Update the index for this diagonal so the next element will be used next time.
                diagIndex.put(key, idx + 1);
            }
        }
        return res;
    }

    public static void main(String[] args) {
        int[][] grid1 = {{1,7,3},{9,8,2},{4,5,6}};
        int[][] grid2 = {{0,1},{1,2}};
        int[][] grid3 = {{1}};
        // Print the sorted matrices for each test case
        System.out.println(Arrays.deepToString(sortMatrixByDiagonals(grid1))); // [[8, 2, 3], [9, 6, 7], [4, 5, 1]]
        System.out.println(Arrays.deepToString(sortMatrixByDiagonals(grid2))); // [[2, 1], [1, 0]]
        System.out.println(Arrays.deepToString(sortMatrixByDiagonals(grid3))); // [[1]]
    }
}

```





