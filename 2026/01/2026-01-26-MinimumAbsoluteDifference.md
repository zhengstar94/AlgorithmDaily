---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1200. Minimum Absolute Difference"
date: "2026-01-26"
tags: Easy
categories:
  - "LeetCode Array"
---


- Given an array of **distinct** integers `arr`, find all pairs of elements with the minimum absolute difference of any two elements.
- Return a list of pairs in ascending order(with respect to pairs), each pair `[a, b]` follows
  - `a, b` are from `arr`
  - `a < b`
  - `b - a` equals to the minimum absolute difference of any two elements in `arr`


**Example 1**

```
Input: arr = [4,2,1,3]
Output: [[1,2],[2,3],[3,4]]
Explanation: The minimum absolute difference is 1. List all pairs with difference equal to 1 in ascending order.
```

**Example 2**

```
Input: arr = [1,3,6,10,15]
Output: [[1,3]]
```

**Example 3**

```
Input: arr = [3,8,-10,23,19,-4,-14,27]
Output: [[-14,-10],[19,23],[23,27]]
```

## Method 1

```tex
【O(nlog(n)) time | O(1) space】
```

```java
package Leetcode.Array;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

/**
 * @Author zhengxingxing
 * @Date 2026/01/26
 */
public class MinimumAbsoluteDifference {

    public static List<List<Integer>> minimumAbsDifference(int[] arr) {
        // 1) Sort the array in ascending order
        Arrays.sort(arr);
        int n = arr.length;
        // 2) Find the minimum difference among all adjacent pairs
        int minDiff = Integer.MAX_VALUE;
        for (int i = 1; i < n; i++) {
            int diff = arr[i] - arr[i - 1];
            if (diff < minDiff) {
                minDiff = diff;
            }
        }
        // 3) Collect all adjacent pairs whose difference equals minDiff
        List<List<Integer>> res = new ArrayList<>();
        for (int i = 1; i < n; i++) {
            if (arr[i] - arr[i - 1] == minDiff) {
                List<Integer> pair = new ArrayList<>(2);
                pair.add(arr[i - 1]);
                pair.add(arr[i]);
                res.add(pair);
            }
        }
        return res;
    }
    public static void main(String[] args) {
        // Test cases
        int[][] tests = {
                {4, 2, 1, 3},                 // Expected: [[1,2],[2,3],[3,4]]
                {1, 3, 6, 10, 15},            // Expected: [[1,3]]
                {3, 8, -10, 23, 19, -4, -14, 27} // Expected: [[-14,-10],[19,23],[23,27]]
        };
        for (int[] test : tests) {
            System.out.println("Input: " + Arrays.toString(test));
            List<List<Integer>> ans = minimumAbsDifference(test);
            System.out.println("Output: " + ans);
            System.out.println();
        }
    }
}

```