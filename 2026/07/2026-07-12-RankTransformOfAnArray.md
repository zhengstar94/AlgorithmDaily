**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1331. Rank Transform of an Array"
date: "2026-07-12"
tags: Easy
categories:
  - "LeetCode Array"
---


- Given an array of integers `arr`, replace each element with its rank.
- The rank represents how large the element is. The rank has the following rules:
  - Rank is an integer starting from 1.
  - The larger the element, the larger the rank. If two elements are equal, their rank must be the same.
  - Rank should be as small as possible.

**Example 1**

```
Input: arr = [40,10,20,30]
Output: [4,1,2,3]
Explanation: 40 is the largest element. 10 is the smallest. 20 is the second smallest. 30 is the third smallest.
```

**Example 2**

```
Input: arr = [100,100,100]
Output: [1,1,1]
Explanation: Same elements share the same rank.
```

**Example 3**

```
Input: arr = [37,12,28,9,100,56,80,5,12]
Output: [5,3,4,2,8,6,7,1,3]
```

## Method 1

```tex
【O(nlogn) time | O(n) space】
```

```java
package Leetcode.Array;

import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

/**
 * @author zhengxingxing
 * @date 2026/07/12
 */
public class RankTransformOfAnArray {

    public static int[] arrayRankTransform(int[] arr) {
        // Create a copy of the original array so that sorting does not
        // modify the input array or destroy its original order.
        int[] sorted = arr.clone();
        Arrays.sort(sorted);

        // Maps each distinct value to its rank.
        Map<Integer, Integer> rank = new HashMap<>();

        // Ranks start from 1.
        int r = 1;

        // Assign ranks to distinct values in ascending order.
        // Duplicate values receive the same rank.
        for (int num : sorted) {
            if (!rank.containsKey(num)) {
                rank.put(num, r++);
            }
        }

        // Construct the answer by replacing each original element
        // with the rank obtained from the map.
        int[] ans = new int[arr.length];
        for (int i = 0; i < arr.length; i++) {
            ans[i] = rank.get(arr[i]);
        }

        return ans;
    }

    public static void main(String[] args) {
        System.out.println(Arrays.toString(
                arrayRankTransform(new int[]{40, 10, 20, 30})));

        System.out.println(Arrays.toString(
                arrayRankTransform(new int[]{100, 100, 100})));

        System.out.println(Arrays.toString(
                arrayRankTransform(new int[]{37, 12, 28, 9, 100, 56, 80, 5, 12})));
    }
}
```