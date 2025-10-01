---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1518. Water Bottles"
date: "2025-10-01"
tags: Easy
categories:
  - "LeetCode Math"
---


- There are `numBottles` water bottles that are initially full of water. You can exchange `numExchange` empty water bottles from the market with one full water bottle.
- The operation of drinking a full water bottle turns it into an empty bottle.
- Given the two integers `numBottles` and `numExchange`, return *the **maximum** number of water bottles you can drink*.

**Example 1**

```
Input: numBottles = 9, numExchange = 3
Output: 13
Explanation: You can exchange 3 empty bottles to get 1 full water bottle.
Number of water bottles you can drink: 9 + 3 + 1 = 13.
```

**Example 2**

```
Input: numBottles = 15, numExchange = 4
Output: 19
Explanation: You can exchange 4 empty bottles to get 1 full water bottle. 
Number of water bottles you can drink: 15 + 3 + 1 = 19.
```

## Method 1

```tex
【O(log(numBottles)) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/10/01
 */
public class WaterBottles {

    public static int numWaterBottles(int numBottles, int numExchange) {
        // totalBottles: Stores the total number of water bottles you can drink, initialized with the starting amount.
        int totalBottles = numBottles;

        // emptyBottles: Stores the number of empty water bottles you currently have. Initially, it's the same as the starting amount.
        int emptyBottles = numBottles;

        // Continue the loop as long as you have enough empty bottles to exchange for new ones.
        while (emptyBottles >= numExchange) {
            // Calculate how many new full water bottles you can get by exchanging your empty bottles.
            int newBottles = emptyBottles / numExchange; // Integer division gives the number of full exchanges possible.

            //  Add the number of newly obtained bottles to the total number of bottles you can drink.
            totalBottles += newBottles;

            // Update the number of empty bottles. This is a critical step.
            // emptyBottles % numExchange:  The number of empty bottles left over AFTER making the exchanges
            // newBottles: The number of *new* empty bottles you get after drinking the bottles you just exchanged for.
            // The new empty bottles are the sum of the empty bottles left over + the number of new bottles drank.
            emptyBottles = emptyBottles % numExchange + newBottles;
        }

        // After the loop finishes, return the maximum number of water bottles you can drink.
        return totalBottles;
    }

    public static void main(String[] args) {
        // Test case 1
        int numBottles1 = 9;
        int numExchange1 = 3;
        int result1 = numWaterBottles(numBottles1, numExchange1);
        System.out.println("Maximum number of water bottles (Example 1): " + result1); // Output: 13

        // Test case 2
        int numBottles2 = 15;
        int numExchange2 = 4;
        int result2 = numWaterBottles(numBottles2, numExchange2);
        System.out.println("Maximum number of water bottles (Example 2): " + result2); // Output: 19

        // Test case 3
        int numBottles3 = 5;
        int numExchange3 = 5;
        int result3 = numWaterBottles(numBottles3, numExchange3);
        System.out.println("Maximum number of water bottles (Example 3): " + result3); // Output: 6
    }
}
```





