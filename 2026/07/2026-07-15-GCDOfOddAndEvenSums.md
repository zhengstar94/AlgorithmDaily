**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3658. GCD of Odd and Even Sums"
date: "2026-07-15"
tags: Easy
categories:
  - "LeetCode Math"
---


- You are given an integer `n`. Your task is to compute the **GCD** (greatest common divisor) of two values:
  - `sumOdd`: the sum of the smallest `n` positive odd numbers.
  - `sumEven`: the sum of the smallest `n` positive even numbers.
- Return the GCD of `sumOdd` and `sumEven`.


**Example 1**

```
Input: n = 4

Output: 4

Explanation:

Sum of the first 4 odd numbers sumOdd = 1 + 3 + 5 + 7 = 16
Sum of the first 4 even numbers sumEven = 2 + 4 + 6 + 8 = 20
Hence, GCD(sumOdd, sumEven) = GCD(16, 20) = 4.
```

**Example 2**

```
Input: n = 5

Output: 5

Explanation:

Sum of the first 5 odd numbers sumOdd = 1 + 3 + 5 + 7 + 9 = 25
Sum of the first 5 even numbers sumEven = 2 + 4 + 6 + 8 + 10 = 30
Hence, GCD(sumOdd, sumEven) = GCD(25, 30) = 5.
```

## Method 1

```tex
【O(1) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2026/07/15
 */
public class GCDOfOddAndEvenSums {


    public static int gcdOfOddEvenSums(int n) {
        return n;
    }


    public static void main(String[] args) {

        // Test case 1
        int n1 = 4;
        System.out.println("Input: " + n1);
        System.out.println("Output: " + gcdOfOddEvenSums(n1));
        System.out.println("Expected: 4");

        System.out.println("----------------");

        // Test case 2
        int n2 = 5;
        System.out.println("Input: " + n2);
        System.out.println("Output: " + gcdOfOddEvenSums(n2));
        System.out.println("Expected: 5");

        System.out.println("----------------");

        // Test case 3
        int n3 = 10;
        System.out.println("Input: " + n3);
        System.out.println("Output: " + gcdOfOddEvenSums(n3));
        System.out.println("Expected: 10");
    }
}
```