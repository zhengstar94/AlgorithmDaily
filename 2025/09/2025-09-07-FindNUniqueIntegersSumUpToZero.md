---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1304. Find N Unique Integers Sum up to Zero"
date: "2025-09-07"
tags: Easy
categories:
  - "LeetCode Math"
---


- Given an integer `n`, return **any** array containing `n` **unique** integers such that they add up to `0`.

**Example 1**

```
Input: n = 5
Output: [-7,-1,1,3,4]
Explanation: These arrays also are accepted [-5,-1,1,2,3] , [-3,-1,2,-2,4].
```

**Example 2**

```
Input: n = 3
Output: [-1,0,1]
```

**Example 3**

```
Input: n = 1
Output: [0]
```

## Method 1

```tex
【O(n) time | O(n) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/09/07
 */
public class FindNUniqueIntegersSumUpToZero {

    public static int[] sumZero(int n) {
        // Create an array to store the result
        int[] res = new int[n];
        // Index to keep track of the current position in the array
        int idx = 0;
        // Add pairs of positive and negative integers
        // For example, for i = 1, add 1 and -1; for i = 2, add 2 and -2, etc.
        // Each pair sums to zero and all numbers are unique
        for (int i = 1; i <= n / 2; i++) {
            res[idx++] = i;    // Add positive integer
            res[idx++] = -i;   // Add its negative counterpart
        }
        // If n is odd, there is one remaining slot to fill
        // Fill it with 0 to ensure the sum is zero and all numbers are unique
        if (n % 2 == 1) {
            res[idx] = 0;
        }
        // Return the resulting array
        return res;
    }

    // Main method to run test cases
    public static void main(String[] args) {
        int[] test1 = sumZero(5); // Example: [-1, 1, -2, 2, 0]
        int[] test2 = sumZero(3); // Example: [-1, 1, 0]
        int[] test3 = sumZero(1); // [0]
        int[] test4 = sumZero(4); // Example: [-1, 1, -2, 2]

        printArray(test1); // Print the result for n = 5
        printArray(test2); // Print the result for n = 3
        printArray(test3); // Print the result for n = 1
        printArray(test4); // Print the result for n = 4
    }
    
    private static void printArray(int[] arr) {
        System.out.print("[");
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i]);
            if (i != arr.length - 1) System.out.print(",");
        }
        System.out.println("]");
    }
}

```





