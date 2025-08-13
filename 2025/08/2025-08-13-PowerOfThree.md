---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "326. Power of Three"
date: "2025-08-13"
tags: Easy
categories:
  - "LeetCode Math"
---


- Given an integer `n`, return *`true` if it is a power of three. Otherwise, return `false`*.
- An integer `n` is a power of three, if there exists an integer `x` such that `n == 3^x`.

**Example 1**

```
Input: n = 27
Output: true
Explanation: 27 = 3^3
```

**Example 2**

```
Input: n = 0
Output: false
Explanation: There is no x where 3^x = 0.
```

**Example 3**

```
Input: n = -1
Output: false
Explanation: There is no x where 3^x = (-1).
```

## Method 1

```tex
【O(1) time | O(1) space】
```

```java
package Leetcode.Array;

/**
 * @Author zhengxingxing
 * @Date 2025/08/13
 */
public class PowerOfThree {

    public static boolean isPowerOfThree(int n) {
        // If n is less than or equal to 0, it cannot be a power of three.
        if (n <= 0) {
            return false;
        }
        // Keep dividing n by 3 as long as it is divisible by 3.
        // This reduces n to its smallest possible value by removing all factors of 3.
        while (n % 3 == 0) {
            n = n / 3;
        }
        // If the final result is 1, then n was a power of three.
        // Otherwise, it was not.
        return n == 1;
    }

    public static void main(String[] args) {
        // Test cases to verify the correctness of the isPowerOfThree method.
        int[] tests = {
                27,   // Expected: true (since 27 = 3^3)
                0,    // Expected: false (0 is not a power of three)
                -1,   // Expected: false (negative numbers cannot be powers of three)
        };
        // Iterate through each test case and print the result.
        for (int n : tests) {
            System.out.println("n = " + n + " -> " + isPowerOfThree(n));
        }
    }
}

```









