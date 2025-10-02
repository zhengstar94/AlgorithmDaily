---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3100. Water Bottles II"
date: "2025-10-02"
tags: Medium
categories:
  - "LeetCode Math"
---


- You are given two integers `numBottles` and `numExchange`.
- `numBottles` represents the number of full water bottles that you initially have. In one operation, you can perform one of the following operations:
  - Drink any number of full water bottles turning them into empty bottles.
  - Exchange `numExchange` empty bottles with one full water bottle. Then, increase `numExchange` by one.
- Note that you cannot exchange multiple batches of empty bottles for the same value of `numExchange`. For example, if `numBottles == 3` and `numExchange == 1`, you cannot exchange `3` empty water bottles for `3` full bottles.
- Return *the **maximum** number of water bottles you can drink*.

**Example 1**

```
Input: numBottles = 13, numExchange = 6
Output: 15
Explanation: The table above shows the number of full water bottles, empty water bottles, the value of numExchange, and the number of bottles drunk.
```

**Example 2**

```
Input: numBottles = 10, numExchange = 3
Output: 13
Explanation: The table above shows the number of full water bottles, empty water bottles, the value of numExchange, and the number of bottles drunk.
```

## Method 1

```tex
【O(numBottles) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/10/02
 */
public class WaterBottlesII {
    
    public static int maxBottlesDrunk(int numBottles, int numExchange) {
        int drunkBottles = numBottles; // Initialize the number of drunk bottles with the initial number of bottles.
        int emptyBottles = numBottles; // Initialize the number of empty bottles with the initial number of bottles.

        // Continue the process as long as there are enough empty bottles to exchange.
        while (emptyBottles >= numExchange) {
            emptyBottles = emptyBottles - numExchange; // Use numExchange empty bottles for an exchange.
            drunkBottles++;             // Drink 1 new bottle.
            emptyBottles++;             // Gain 1 more empty bottle after drinking.
            numExchange++;              // The exchange rate increases for the next exchange.
        }

        return drunkBottles; // Return the total number of bottles drunk.
    }

    public static void main(String[] args) {
        // Test Case 1
        int numBottles1 = 13;
        int numExchange1 = 6;
        int result1 = maxBottlesDrunk(numBottles1, numExchange1);
        System.out.println("Example 1: numBottles = " + numBottles1 + ", numExchange = " + numExchange1 + ", Result = " + result1); // Output: 15

        // Test Case 2
        int numBottles2 = 10;
        int numExchange2 = 3;
        int result2 = maxBottlesDrunk(numBottles2, numExchange2);
        System.out.println("Example 2: numBottles = " + numBottles2 + ", numExchange = " + numExchange2 + ", Result = " + result2); // Output: 13
    }
}
```





