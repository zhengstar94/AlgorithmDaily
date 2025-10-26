---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1716. Calculate Money in Leetcode Bank"
date: "2025-10-26"
tags: Easy
categories:
  - "LeetCode Math"
---


- Hercy wants to save money for his first car. He puts money in the Leetcode bank **every day**.
- He starts by putting in `$1` on Monday, the first day. Every day from Tuesday to Sunday, he will put in `$1` more than the day before. On every subsequent Monday, he will put in `$1` more than the **previous Monday**.
- Given `n`, return *the total amount of money he will have in the Leetcode bank at the end of the* `nth` *day.*

**Example 1**

```
Input: n = 4
Output: 10
Explanation: After the 4th day, the total is 1 + 2 + 3 + 4 = 10.
```

**Example 2**

```
Input: n = 10
Output: 37
Explanation: After the 10th day, the total is (1 + 2 + 3 + 4 + 5 + 6 + 7) + (2 + 3 + 4) = 37. Notice that on the 2nd Monday, Hercy only puts in $2.
```

**Example 3**

```
Input: n = 20
Output: 96
Explanation: After the 20th day, the total is (1 + 2 + 3 + 4 + 5 + 6 + 7) + (2 + 3 + 4 + 5 + 6 + 7 + 8) + (3 + 4 + 5 + 6 + 7 + 8) = 96.
```

## Method 1

```tex
【O(1) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/10/26
 */
public class CalculateMoneyInLeetcodeBank {
    
    public static int totalMoney(int n) {
        final int D = 7; // The number of days in a week
        int weeks = n / D;      // The number of full weeks within 'n' days
        int remainingDays = n % D;      // The number of remaining days after accounting for full weeks

        // Calculate the total money saved during the full weeks
        // This formula efficiently computes the sum based on the increasing deposit pattern.
        int totalForFullWeeks = weeks * D * (weeks + D) / 2;

        // Calculate the total money saved during the remaining days
        // This accounts for the increasing deposits in the partial week.
        int totalForRemainingDays = remainingDays * (weeks * 2 + remainingDays + 1) / 2;

        // Calculate the total money saved (full weeks + remaining days)
        return totalForFullWeeks + totalForRemainingDays;
    }

    public static void main(String[] args) {
        // Test cases to verify the correctness of the totalMoney method
        System.out.println("n = 4, Total Money: " + totalMoney(4));   // Expected Output: 10
        System.out.println("n = 10, Total Money: " + totalMoney(10)); // Expected Output: 37
        System.out.println("n = 20, Total Money: " + totalMoney(20)); // Expected Output: 96
        System.out.println("n = 28, Total Money: " + totalMoney(28)); // Expected Output: 196
    }
}

```





