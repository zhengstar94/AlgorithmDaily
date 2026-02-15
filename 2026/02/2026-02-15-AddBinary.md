**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "67. Add Binary"
date: "2026-02-15"
tags: Easy
categories:
  - "LeetCode String"
---


- Given two binary strings `a` and `b`, return *their sum as a binary string*.

**Example 1**

```
Input: a = "11", b = "1"
Output: "100"
```

**Example 2**

```
Input: a = "1010", b = "1011"
Output: "10101"
```

## Method 1

```tex
【O(n) time | O(n) space】
```

```java
package Leetcode.String;

/**
 * @Author zhengxingxing
 * @Date 2026/02/15
 */
public class AddBinary {

    public static String addBinary(String a, String b) {
        // Stores result bits as we compute them from low bit to high bit.
        // We reverse it at the end to get the final correct order.
        StringBuilder result = new StringBuilder();

        // Pointer to the last character of a (least significant bit of a).
        int i = a.length() - 1;

        // Pointer to the last character of b (least significant bit of b).
        int j = b.length() - 1;

        // Carry from the previous bit addition (either 0 or 1 in binary addition).
        int carry = 0;

        // Continue while:
        // 1) a still has bits, or
        // 2) b still has bits, or
        // 3) there is still a carry to process
        while (i >= 0 || j >= 0 || carry > 0) {
            // Start this round with previous carry.
            int sum = carry;

            // If a still has a bit at index i, convert char ('0'/'1') to int (0/1) and add it.
            if (i >= 0) {
                sum += a.charAt(i) - '0';
                i--; // Move to the next higher bit in a.
            }

            // If b still has a bit at index j, convert char ('0'/'1') to int (0/1) and add it.
            if (j >= 0) {
                sum += b.charAt(j) - '0';
                j--; // Move to the next higher bit in b.
            }

            // Append the current output bit.
            // In binary, current bit is sum modulo 2.
            result.append(sum % 2);

            // Compute carry for the next position.
            // In binary, carry is sum divided by 2 (integer division).
            carry = sum / 2;
        }

        // Bits were appended from least significant to most significant,
        // so reverse to return normal binary order.
        return result.reverse().toString();
    }

    public static void main(String[] args) {
        // Test case 1
        String a1 = "11";
        String b1 = "1";
        System.out.println("Input: a = \"" + a1 + "\", b = \"" + b1 + "\"");
        System.out.println("Output: " + addBinary(a1, b1)); // Expected: 100

        // Test case 2
        String a2 = "1010";
        String b2 = "1011";
        System.out.println("Input: a = \"" + a2 + "\", b = \"" + b2 + "\"");
        System.out.println("Output: " + addBinary(a2, b2)); // Expected: 10101
    }
}
```