**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "2839. Check if Strings Can be Made Equal With Operations I"
date: "2026-03-29"
tags: Easy
categories:
  - "LeetCode Math"
---


- You are given two strings `s1` and `s2`, both of length `4`, consisting of **lowercase** English letters.
- You can apply the following operation on any of the two strings **any** number of times:
  - Choose any two indices `i` and `j` such that `j - i = 2`, then **swap** the two characters at those indices in the string.
- Return `true` *if you can make the strings* `s1` *and* `s2` *equal, and* `false` *otherwise*.

**Example 1**

```
Input: s1 = "abcd", s2 = "cdab"
Output: true
Explanation: We can do the following operations on s1:
- Choose the indices i = 0, j = 2. The resulting string is s1 = "cbad".
- Choose the indices i = 1, j = 3. The resulting string is s1 = "cdab" = s2.
```

**Example 2**

```
Input: s1 = "abcd", s2 = "dacb"
Output: false
Explanation: It is not possible to make the two strings equal.
```

## Method 1

```tex
【O(1) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2026/03/29
 */
public class CheckIfStringsCanBeMadeEqualWithOperationsI {
    public static boolean canBeEqual(String s1, String s2) {
        return sameGroup(s1.charAt(0), s1.charAt(2), s2.charAt(0), s2.charAt(2))
                && sameGroup(s1.charAt(1), s1.charAt(3), s2.charAt(1), s2.charAt(3));
    }
    
    public static boolean sameGroup(char a1, char a2, char b1, char b2) {
        return (a1 == b1 && a2 == b2) || (a1 == b2 && a2 == b1);
    }

    public static void main(String[] args) {
        String s1 = "abcd";
        String s2 = "cdab";
        System.out.println("Test 1:");
        System.out.println("Input: s1 = " + s1 + ", s2 = " + s2);
        System.out.println("Output: " + canBeEqual(s1, s2));
        System.out.println("Expected: true");
        System.out.println();

        String s3 = "abcd";
        String s4 = "dacb";
        System.out.println("Test 2:");
        System.out.println("Input: s1 = " + s3 + ", s2 = " + s4);
        System.out.println("Output: " + canBeEqual(s3, s4));
        System.out.println("Expected: false");
        System.out.println();
    }
}

```