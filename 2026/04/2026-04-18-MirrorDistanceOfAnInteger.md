**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3783. Mirror Distance of an Integer"
date: "2026-04-18"
tags: Easy
categories:
  - "LeetCode Math"
---


- You are given an integer `n`.

- Define its **mirror distance** as: `abs(n - reverse(n))` where `reverse(n)` is the integer formed by reversing the digits of `n`.

- Return an integer denoting the mirror distance of `n`.

- abs(x)` denotes the absolute value of `x`.



**Example 1**

```
Input: n = 25

Output: 27

Explanation:

reverse(25) = 52.
Thus, the answer is abs(25 - 52) = 27.
```

**Example 2**

```
Input: n = 10

Output: 9

Explanation:

reverse(10) = 01 which is 1.
Thus, the answer is abs(10 - 1) = 9.
```

**Example 3**

```
Input: n = 7

Output: 0

Explanation:

reverse(7) = 7.
Thus, the answer is abs(7 - 7) = 0.
```

## Method 1

```tex
【O(log(n)) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2026/04/18
 */
public class MirrorDistanceOfAnInteger {
    
    public static int mirrorDistance(int n) {
        // Use a 'long' to store the reversed number. This is a crucial step to
        // prevent integer overflow. For example, if n = 1534236469, its reverse
        // is 9646324351, which is larger than Integer.MAX_VALUE.
        long reversedN = 0;

        // Loop through the digits of the original number 'n'.
        // We use a temporary variable 'tempN' so that the original 'n' remains unchanged for the final calculation.
        // The loop continues as long as there are digits left in tempN (i.e., tempN > 0).
        // In each iteration, we remove the last digit of tempN by integer division (tempN /= 10).
        for (int tempN = n; tempN > 0; tempN /= 10) {
            // This is the core logic to reverse the number:
            // 1. `tempN % 10`: This extracts the last digit of the current number (e.g., gets 3 from 123).
            // 2. `reversedN * 10`: This "shifts" the existing reversed number to the left
            //    by one decimal place, making room for the new digit (e.g., turns 21 into 210).
            // 3. `... + ...`: The extracted last digit is then added to the empty spot.
            reversedN = reversedN * 10 + tempN % 10;
        }

        // Calculate the absolute difference between the original number and its reversed form.
        // During the subtraction `n - reversedN`, the `int n` is automatically promoted to `long`
        // to match the type of `reversedN`. `Math.abs()` then operates on the `long` result.
        // Finally, the result is cast back to `int` as required by the method signature.
        return (int) Math.abs(n - reversedN);
    }
    
    public static void main(String[] args) {
        // --- Basic Test Cases ---

        int n1 = 25;
        System.out.println("Input: " + n1 + ", Output: " + mirrorDistance(n1)); // Expected: 27

        int n2 = 10;
        System.out.println("Input: " + n2 + ", Output: " + mirrorDistance(n2)); // Expected: 9

        int n3 = 7;
        System.out.println("Input: " + n3 + ", Output: " + mirrorDistance(n3));  // Expected: 0
    }
}
```