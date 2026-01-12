---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1266. Minimum Time Visiting All Points"
date: "2026-01-12"
tags: Easy
categories:
  - "LeetCode Greedy"
---


- On a 2D plane, there are `n` points with integer coordinates `points[i] = [xi, yi]`. Return *the **minimum time** in seconds to visit all the points in the order given by* `points`.
- You can move according to these rules:
  - In `1` second, you can either:
    - move vertically by one unit,
    - move horizontally by one unit, or
    - move diagonally `sqrt(2)` units (in other words, move one unit vertically then one unit horizontally in `1` second).
  - You have to visit the points in the same order as they appear in the array.
  - You are allowed to pass through points that appear later in the order, but these do not count as visits.


**Example 1**

```
Input: points = [[1,1],[3,4],[-1,0]]
Output: 7
Explanation: One optimal path is [1,1] -> [2,2] -> [3,3] -> [3,4] -> [2,3] -> [1,2] -> [0,1] -> [-1,0]   
Time from [1,1] to [3,4] = 3 seconds 
Time from [3,4] to [-1,0] = 4 seconds
Total time = 7 seconds
```

**Example 2**

```
Input: points = [[3,2],[-2,2]]
Output: 5
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Greedy;

/**
 * @Author zhengxingxing
 * @Date 2026/01/12
 */
public class MinimumTimeVisitingAllPoints {


    public static int minTimeToVisitAllPoints(int[][] points) {
        int totalTime = 0; // Initialize the total time to 0

        // Iterate through the points array, starting from the second point (index 1)
        // because we need to calculate the time between consecutive points.
        for (int i = 1; i < points.length; i++) {
            // Get the coordinates of the previous point
            int x1 = points[i - 1][0]; // x-coordinate of the previous point
            int y1 = points[i - 1][1]; // y-coordinate of the previous point

            // Get the coordinates of the current point
            int x2 = points[i][0]; // x-coordinate of the current point
            int y2 = points[i][1]; // y-coordinate of the current point

            // Calculate the absolute differences in x and y coordinates.
            // These represent the horizontal and vertical distances between the two points.
            int dx = Math.abs(x2 - x1); // Absolute difference in x-coordinates
            int dy = Math.abs(y2 - y1); // Absolute difference in y-coordinates

            // The minimum time to travel between two points is the maximum of the
            // absolute differences in x and y coordinates. This is because we can move
            // diagonally in one second, which covers one unit in both x and y directions.
            // Therefore, we take the larger of the two distances to determine the time.
            totalTime += Math.max(dx, dy); // Add the time for this segment to the total time
        }

        return totalTime; // Return the total time required to visit all points
    }


    public static void main(String[] args) {
        // Test case 1
        int[][] points1 = {{1, 1}, {3, 4}, {-1, 0}};
        System.out.println(minTimeToVisitAllPoints(points1)); // Output: 7

        // Test case 2
        int[][] points2 = {{3, 2}, {-2, 2}};
        System.out.println(minTimeToVisitAllPoints(points2)); // Output: 5
    }
}

```





