**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "796. Rotate String"
date: "2026-05-03"
tags: Easy
categories:
  - "LeetCode Array"
---


- Given two strings `s` and `goal`, return `true` *if and only if* `s` *can become* `goal` *after some number of **shifts** on* `s`.

- A **shift** on `s` consists of moving the leftmost character of `s` to the rightmost position.

  - For example, if `s = "abcde"`, then it will be `"bcdea"` after one shift.




**Example 1**

```
Input: s = "abcde", goal = "cdeab"
Output: true
```

**Example 2**

```
Input: s = "abcde", goal = "abced"
Output: false
```

## Method 1

```tex
【O(n^2) time | O(n) space】
```

```java
package Leetcode.Array;

/**
 * @author zhengxingxing
 * @date 2026/05/03
 */
public class RotateString {


    public static boolean rotateString(String s, String goal) {
        // The core logic is based on two conditions:
        // 1. The lengths of 's' and 'goal' must be equal. If not, it's impossible for
        //    's' to become 'goal' through rotation, so we can immediately return false.
        //
        // 2. If 'goal' is a rotation of 's', then 'goal' must be a substring of 's'
        //    concatenated with itself (s + s).
        //
        //    Example:
        //    If s = "abcde", then s + s = "abcdeabcde".
        //    All possible rotations of "s" are present in "abcdeabcde":
        //    - "abcde"
        //    - "bcdea"
        //    - "cdeab"
        //    - "deabc"
        //    - "eabcd"
        //    So, we just need to check if 'goal' is contained within this concatenated string.
        return s.length() == goal.length() && (s + s).contains(goal);
    }

    public static void main(String[] args) {
        System.out.println(rotateString("abcde", "cdeab")); // Expected output: true
        
        System.out.println(rotateString("abcde", "abced")); // Expected output: false
    }
}
```