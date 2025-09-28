---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "976. Largest Perimeter Triangle"
date: "2025-09-28"
tags: Easy
categories:
  - "LeetCode Math"
---


- Given an integer array `nums`, return *the largest perimeter of a triangle with a non-zero area, formed from three of these lengths*. If it is impossible to form any triangle of a non-zero area, return `0`.


**Example 1**

```
Input: nums = [2,1,2]
Output: 5
Explanation: You can form a triangle with three side lengths: 1, 2, and 2.
```

**Example 2**

```
Input: nums = [1,2,1,10]
Output: 0
Explanation: 
You cannot use the side lengths 1, 1, and 2 to form a triangle.
You cannot use the side lengths 1, 1, and 10 to form a triangle.
You cannot use the side lengths 1, 2, and 10 to form a triangle.
As we cannot use any three side lengths to form a triangle of non-zero area, we return 0.
```

## Method 1

```tex
【O(n*log(n)) time | O(1) space】
```

```java
package Leetcode.Math;

import java.util.Arrays;

/**
 * @Author zhengxingxing
 * @Date 2025/09/28
 */
public class LargestPerimeterTriangle {

    public static int largestPerimeter(int[] nums) {
        // Step 1: Sort the array in ascending order
        // Sorting helps because we only need to check the largest values 
        // (triangle inequality is most likely to hold for larger numbers).
        Arrays.sort(nums);

        // Step 2: Iterate from the end of the sorted array
        // We check triplets in descending order of size to maximize the perimeter.
        for (int i = nums.length - 1; i >= 2; i--) {
            // Let the three sides be: nums[i-2], nums[i-1], nums[i]
            // Triangle inequality: the sum of any two sides must be greater than the third.
            // Since the array is sorted, nums[i] is the largest side.
            if (nums[i - 2] + nums[i - 1] > nums[i]) {
                // Valid triangle found: return its perimeter
                return nums[i - 2] + nums[i - 1] + nums[i];
            }
        }

        // Step 3: If no valid triangle is found, return 0
        return 0;
    }

    public static void main(String[] args) {
        // Example 1: nums = [2, 1, 2]
        // Sorted -> [1, 2, 2]
        // 1 + 2 > 2 (true), so perimeter = 1 + 2 + 2 = 5
        int[] nums1 = {2, 1, 2};
        System.out.println("Input: " + Arrays.toString(nums1)
                + ", Largest Perimeter: " + largestPerimeter(nums1)); // Output: 5

        // Example 2: nums = [1, 2, 1, 10]
        // Sorted -> [1, 1, 2, 10]
        // Check (1,2,10): 1+2=3 <= 10 -> not valid
        // Check (1,1,2): 1+1=2 <= 2  -> not valid
        // No valid triangle, so result = 0
        int[] nums2 = {1, 2, 1, 10};
        System.out.println("Input: " + Arrays.toString(nums2)
                + ", Largest Perimeter: " + largestPerimeter(nums2)); // Output: 0
    }
}

```





