---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "812. Largest Triangle Area"
date: "2025-09-28"
tags: Easy
categories:
  - "LeetCode Math"
---

- Given an array of points on the **X-Y** plane `points` where `points[i] = [xi, yi]`, return *the area of the largest triangle that can be formed by any three different points*. Answers within `10-5` of the actual answer will be accepted.


**Example 1**

```
Input: points = [[0,0],[0,1],[1,0],[0,2],[2,0]]
Output: 2.00000
Explanation: The five points are shown in the above figure. The red triangle is the largest.
```

**Example 2**

```
Input: points = [[1,0],[0,0],[0,1]]
Output: 0.50000
```

## Method 1

```tex
【O(n^3) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/09/28
 */
public class LargestTriangleArea {

    public static double largestTriangleArea(int[][] points) {
        int n = points.length;  // total number of points
        int ans = 0;  // store twice the maximum area (to avoid precision issues with division until the end)

        // Choose 3 different points (i, j, k) to form a triangle
        // Outer loop: pick the first point (i)
        for (int i = 0; i < n - 2; i++) {
            // Middle loop: pick the second point (j), must be after i
            for (int j = i + 1; j < n - 1; j++) {
                // Inner loop: pick the third point (k), must be after j
                for (int k = j + 1; k < n; k++) {
                    // Extract the three points
                    int[] p1 = points[i];
                    int[] p2 = points[j];
                    int[] p3 = points[k];

                    // Build two vectors:
                    // Vector a = p2 - p1
                    int x1 = p2[0] - p1[0];
                    int y1 = p2[1] - p1[1];

                    // Vector b = p3 - p1
                    int x2 = p3[0] - p1[0];
                    int y2 = p3[1] - p1[1];

                    /**
                     * Compute the cross product of vectors a and b:
                     *      a × b = x1 * y2 - x2 * y1
                     *
                     * Geometric meaning:
                     * - |a × b| = area of the parallelogram formed by vectors a and b
                     * - Therefore, the area of the triangle = |a × b| / 2
                     *
                     * We use Math.abs(...) to ensure the area is positive,
                     * and Math.max(...) to keep track of the largest area found so far.
                     *
                     * Note: Here we store "twice the area" in ans (no division by 2 yet),
                     * to avoid losing precision with floating-point division until the very end.
                     */
                    ans = Math.max(ans, Math.abs(x1 * y2 - x2 * y1));
                }
            }
        }

        // Divide by 2.0 at the end to get the actual triangle area
        return ans / 2.0;
    }

    public static void main(String[] args) {
        // Example 1: Points include (0,0), (0,1), (1,0), (0,2), (2,0)
        // The largest triangle is between (0,2), (2,0), and (0,0), with area = 2.0
        int[][] points1 = {{0, 0}, {0, 1}, {1, 0}, {0, 2}, {2, 0}};
        System.out.println("Example 1: " + largestTriangleArea(points1)); // Output: 2.0

        // Example 2: Points are (1,0), (0,0), (0,1)
        // The triangle is a simple right triangle with area = 0.5
        int[][] points2 = {{1, 0}, {0, 0}, {0, 1}};
        System.out.println("Example 2: " + largestTriangleArea(points2)); // Output: 0.5
    }
}

```





