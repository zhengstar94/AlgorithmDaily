---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "717. 1-bit and 2-bit Characters"
date: "2025-11-18"
tags: Easy
categories:
  - "LeetCode Math"
---


- We have two special characters:
  - The first character can be represented by one bit `0`.
  - The second character can be represented by two bits (`10` or `11`).
- Given a binary array `bits` that ends with `0`, return `true` if the last character must be a one-bit character.


**Example 1**

```
Input: bits = [1,0,0]
Output: true
Explanation: The only way to decode it is two-bit character and one-bit character.
So the last character is one-bit character.
```

**Example 2**

```
Input: bits = [1,1,1,0]
Output: false
Explanation: The only way to decode it is two-bit character and two-bit character.
So the last character is not one-bit character.
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/11/18
 */
public class OneBitTwoBitCharacters {
    public static boolean isOneBitCharacter(int[] bits) {
        int i = 0;
        while (i < bits.length - 1) { // Iterate up to the second to last element
            if (bits[i] == 1) {
                i += 2; // If it's a two-bit character (10 or 11), skip two bits
            } else {
                i++; // If it's a one-bit character (0), skip one bit
            }
        }
        return i == bits.length - 1; // Check if the last character is reached after decoding
    }

    public static void main(String[] args) {
        // Test cases
        int[] bits1 = {1, 0, 0};
        System.out.println("Test Case 1: " + isOneBitCharacter(bits1)); // Output: true
        int[] bits2 = {1, 1, 1, 0};
        System.out.println("Test Case 2: " + isOneBitCharacter(bits2)); // Output: false
    }
}

```





