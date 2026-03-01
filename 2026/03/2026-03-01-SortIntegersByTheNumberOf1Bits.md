**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "356. Sort Integers by The Number of 1 Bits"
date: "2026-03-01"
tags: Medium
categories:
  - "LeetCode String"
---


- A decimal number is called **deci-binary** if each of its digits is either `0` or `1` without any leading zeros. For example, `101` and `1100` are **deci-binary**, while `112` and `3001` are not.
- Given a string `n` that represents a positive decimal integer, return *the **minimum** number of positive **deci-binary** numbers needed so that they sum up to* `n`*.*


**Example 1**

```
Input: n = "32"
Output: 3
Explanation: 10 + 11 + 11 = 32
```

**Example 2**

```
Input: n = "82734"
Output: 8
```

**Example 3**

```
Input: n = "27346209830709182346"
Output: 9
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.String;

/**
 * @Author zhengxingxing
 * @Date 2026/03/01
 */
public class SortIntegersByTheNumberOf1Bits {

    public static int minPartitions(String n) {
        // Initialize max digit as 0
        int mx = 0;

        // Iterate through each character in the string
        for (char ch : n.toCharArray()) {
            // Compare ASCII values to find the maximum digit character
            // Since digits 0-9 have consecutive ASCII codes, comparing chars gives correct ordering
            mx = Math.max(mx, ch);
        }

        // Convert the maximum character to its numeric value by subtracting ASCII '0'
        // Example: '5' (ASCII 53) - '0' (ASCII 48) = 5
        return mx - '0';
    }
    
    public static void main(String[] args) {
        // Test cases

        // Case 1: Should return 3 (digits are 3,2; max is 3)
        System.out.println(minPartitions("32"));      // Expected output: 3

        // Case 2: Should return 8 (digits are 8,2,7,3,4; max is 8)
        System.out.println(minPartitions("82734"));   // Expected output: 8

        // Case 3: Should return 9 (contains two 9s, which is the largest digit)
        System.out.println(minPartitions("27346209830709182346")); // Expected output: 9
    }
}
```