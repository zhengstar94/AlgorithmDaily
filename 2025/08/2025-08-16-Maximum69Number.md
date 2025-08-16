---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1323. Maximum 69 Number"
date: "2025-08-16"
tags: Easy
categories:
  - "LeetCode Math"
---


- You are given a positive integer `num` consisting only of digits `6` and `9`.
- Return *the maximum number you can get by changing **at most** one digit (*`6` *becomes* `9`*, and* `9` *becomes* `6`*)*.

**Example 1**

```
Input: num = 9669
Output: 9969
Explanation: 
Changing the first digit results in 6669.
Changing the second digit results in 9969.
Changing the third digit results in 9699.
Changing the fourth digit results in 9666.
The maximum number is 9969.
```

**Example 2**

```
Input: num = 9996
Output: 9999
Explanation: Changing the last digit 6 to 9 results in the maximum number.
```

**Example 3**

```
Input: num = 9999
Output: 9999
Explanation: It is better not to apply any change.
```

## Method 1

```tex
【O(n) time | O(n) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/08/16
 */
public class Maximum69Number {
    public static int maximum69Number (int num) {
        // Convert the integer to a character array for easy modification of digits
        char[] chars = Integer.toString(num).toCharArray();
        // Traverse each digit from left to right (from the highest digit)
        for (int i = 0; i < chars.length; i++) {
            // If the current digit is '6', change it to '9'
            if (chars[i] == '6') {
                chars[i] = '9';
                // Only one change is allowed, so break after the first change
                break;
            }
        }
        // Convert the modified character array back to an integer and return
        return Integer.parseInt(new String(chars));
    }

    public static void main(String[] args) {
        // Test case 1: Changing the second digit '6' to '9' gives 9969
        System.out.println(maximum69Number(9669)); // Output: 9969
        // Test case 2: Changing the last digit '6' to '9' gives 9999
        System.out.println(maximum69Number(9996)); // Output: 9999
        // Test case 3: No change needed, already the maximum
        System.out.println(maximum69Number(9999)); // Output: 9999
        // Test case 4: Changing the first digit '6' to '9' gives 9969
        System.out.println(maximum69Number(6969)); // Output: 9969
    }
}

```





