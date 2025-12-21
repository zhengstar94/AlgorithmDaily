---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "944. Delete Columns to Make Sorted"
date: "2025-12-21"
tags: Easy
categories:
  - "LeetCode Array"
---

- You are given an array of `n` strings `strs`, all of the same length.

- The strings can be arranged such that there is one on each line, making a grid.

  - For example, `strs = ["abc", "bce", "cae"]` can be arranged as follows:

    > abc
    >
    > bce
    >
    > Cae

- You want to **delete** the columns that are **not sorted lexicographically**. In the above example (**0-indexed**), columns 0 (`'a'`, `'b'`, `'c'`) and 2 (`'c'`, `'e'`, `'e'`) are sorted, while column 1 (`'b'`, `'c'`, `'a'`) is not, so you would delete column 1.

- Return *the number of columns that you will delete*.

**Example 1**

```
Input: strs = ["cba","daf","ghi"]
Output: 1
Explanation: The grid looks as follows:
  cba
  daf
  ghi
Columns 0 and 2 are sorted, but column 1 is not, so you only need to delete 1 column.
```

**Example 2**

```
Input: strs = ["a","b"]
Output: 0
Explanation: The grid looks as follows:
  a
  b
Column 0 is the only column and is sorted, so you will not delete any columns.
```

**Example 3**

```
Input: strs = ["zyx","wvu","tsr"]
Output: 3
Explanation: The grid looks as follows:
  zyx
  wvu
  tsr
All 3 columns are not sorted, so you will delete all 3.
```

## Method 1

```tex
【O(mn) time | O(1) space】
```

```java
package Leetcode.Array;

/**
 * @Author zhengxingxing
 * @Date 2025/12/21
 */
public class DeleteColumnsToMakeSorted {

    public static int minDeletionSize(String[] strs) {
        int n = strs.length; // Get the length of the string array, which is the number of rows
        int m = strs[0].length(); // Get the length of each string, which is the number of columns
        int ans = 0; // Initialize the number of columns to delete to 0

        // Iterate through each column
        for (int j = 0; j < m; j++) {
            // Iterate through the letters in column j, starting from the second row (because we need to compare with the previous row)
            for (int i = 1; i < n; i++) {
                // If the character in the current row is less than the character in the previous row,
                // it means the column is not lexicographically increasing.
                if (strs[i - 1].charAt(j) > strs[i].charAt(j)) {
                    ans++; // Increment the number of columns to delete
                    break; // Exit the inner loop because we have already determined that this column needs to be deleted
                }
            }
        }
        return ans; // Return the number of columns to delete
    }

    public static void main(String[] args) {
        // Test cases
        String[] strs1 = {"cba", "daf", "ghi"};
        System.out.println("Number of columns to delete: " + minDeletionSize(strs1)); // Output: 1

        String[] strs2 = {"a", "b"};
        System.out.println("Number of columns to delete: " + minDeletionSize(strs2)); // Output: 0

        String[] strs3 = {"zyx", "wvu", "tsr"};
        System.out.println("Number of columns to delete: " + minDeletionSize(strs3)); // Output: 3

        String[] strs4 = {"abc", "bce", "cae"};
        System.out.println("Number of columns to delete: " + minDeletionSize(strs4)); // Output: 1
    }
}

```





