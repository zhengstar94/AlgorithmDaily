---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3228. Maximum Number of Operations to Move Ones to the End"
date: "2025-11-13"
tags: Medium
categories:
  - "LeetCode Math"
---


- You are given a binary string `s`.

- You can perform the following operation on the string **any** number of times:

  - Choose **any** index `i` from the string where `i + 1 < s.length` such that `s[i] == '1'` and `s[i + 1] == '0'`.
  - Move the character `s[i]` to the **right** until it reaches the end of the string or another `'1'`. For example, for `s = "010010"`, if we choose `i = 1`, the resulting string will be `s = "0**001**10"`.

- Return the **maximum** number of operations that you can perform.



**Example 1**

```
Input: s = "1001101"

Output: 4

Explanation:

We can perform the following operations:

- Choose index i = 0. The resulting string is s = "0011101".
- Choose index i = 4. The resulting string is s = "0011011".
- Choose index i = 3. The resulting string is s = "0010111".
- Choose index i = 2. The resulting string is s = "0001111".
```

**Example 2**

```
Input: s = "00111"

Output: 0
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/11/13
 */
public class MaximumNumberOfOperationsToMoveOnesToTheEnd {
    
    public static int maxOperations(String S) {
        // Convert the string to a character array for easier access.
        char[] s = S.toCharArray();

        // 'ans' stores the total number of operations that can be performed.
        int ans = 0;

        // 'cnt1' keeps track of the number of consecutive '1's encountered so far.
        int cnt1 = 0;

        // Iterate through the character array.
        for (int i = 0; i < s.length; i++) {
            // If the current character is '1', increment the count of consecutive '1's.
            if (s[i] == '1') {
                cnt1++;
            }
            // If the current character is '0' AND the previous character was '1',
            // it means we've found a "10" pattern, and we can perform 'cnt1' operations
            // to move all the previous consecutive '1's to the end (conceptually, after this '0').
            else if (i > 0 && s[i - 1] == '1') {
                ans += cnt1; // Add the count of previous '1's to the total operations.
            }
        }

        // Return the total number of operations.
        return ans;
    }

    public static void main(String[] args) {
        // Test cases:

        // Test case 1
        String s1 = "1001101";
        System.out.println("Input: " + s1 + ", Output: " + maxOperations(s1)); // Expected Output: 4

        // Test case 2
        String s2 = "00111";
        System.out.println("Input: " + s2 + ", Output: " + maxOperations(s2)); // Expected Output: 0
    }
}

```





