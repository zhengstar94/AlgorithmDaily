**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1833. Maximum Ice Cream Bars"
date: "2026-06-21"
tags: Medium
categories:
  - "LeetCode Greedy"
---


- It is a sweltering summer day, and a boy wants to buy some ice cream bars.
- At the store, there are `n` ice cream bars. You are given an array `costs` of length `n`, where `costs[i]` is the price of the `ith` ice cream bar in coins. The boy initially has `coins` coins to spend, and he wants to buy as many ice cream bars as possible.
- **Note:** The boy can buy the ice cream bars in any order.
- Return *the **maximum** number of ice cream bars the boy can buy with* `coins` *coins.*
- You must solve the problem by counting sort.

**Example 1**

```
Input: costs = [1,3,2,4,1], coins = 7
Output: 4
Explanation: The boy can buy ice cream bars at indices 0,1,2,4 for a total price of 1 + 3 + 2 + 1 = 7.
```

**Example 2**

```
Input: costs = [10,6,8,7,7,8], coins = 5
Output: 0
Explanation: The boy cannot afford any of the ice cream bars.
```

**Example 3**

```
Input: costs = [1,6,3,1,2,5], coins = 20
Output: 6
Explanation: The boy can buy all the ice cream bars for a total price of 1 + 6 + 3 + 1 + 2 + 5 = 18.
```

## Method 1

```tex
【O(nlogn) time | O(1) space】
```

```java
package Leetcode.Greedy;

import java.util.Arrays;

/**
 * @Author zhengxingxing
 * @Date 2026/06/21
 */
public class MaximumIceCreamBars {

    public static int maxIceCream(int[] costs, int coins) {
        if (costs == null || costs.length == 0 || coins <= 0) {
            return 0;
        }

        // Step 1: Find the maximum price (required for counting sort array size)
        int maxPrice = 0;
        for (int cost : costs) {
            if (cost > maxPrice) {
                maxPrice = cost;
            }
        }

        // Step 2: Counting sort via frequency array (O(n) time)
        int[] freq = new int[maxPrice + 1];
        for (int cost : costs) {
            freq[cost]++;
        }

        int totalBought = 0;

        // Step 3: Greedy traversal from cheapest to most expensive
        for (int price = 0; price <= maxPrice; price++) {
            // If there are multiple bars of this price
            for (int i = 0; i < freq[price]; i++) {
                if (coins < price) {
                    // Not enough coins for this or any remaining bar
                    return totalBought;
                }
                coins -= price;   // Pay for the bar
                totalBought++;    // Count this bar
            }
        }

        // If we reach here, we bought all bars
        return totalBought;
    }


    public static void main(String[] args) {
        // Test case 1 (Example 1)
        int[] costs1 = {1, 3, 2, 4, 1};
        int coins1 = 7;
        int result1 = maxIceCream(costs1, coins1);
        System.out.println("Test case 1: costs = " + Arrays.toString(costs1) + ", coins = " + coins1);
        System.out.println("Expected output: 4");
        System.out.println("Actual output: " + result1);
        System.out.println("Correct? " + (result1 == 4));
        System.out.println("--------------------");

        // Test case 2 (Example 2)
        int[] costs2 = {10, 6, 8, 7, 7, 8};
        int coins2 = 5;
        int result2 = maxIceCream(costs2, coins2);
        System.out.println("Test case 2: costs = " + Arrays.toString(costs2) + ", coins = " + coins2);
        System.out.println("Expected output: 0");
        System.out.println("Actual output: " + result2);
        System.out.println("Correct? " + (result2 == 0));
        System.out.println("--------------------");

        // Test case 3 (Example 3)
        int[] costs3 = {1, 6, 3, 1, 2, 5};
        int coins3 = 20;
        int result3 = maxIceCream(costs3, coins3);
        System.out.println("Test case 3: costs = " + Arrays.toString(costs3) + ", coins = " + coins3);
        System.out.println("Expected output: 6");
        System.out.println("Actual output: " + result3);
        System.out.println("Correct? " + (result3 == 6));
        System.out.println("--------------------");
    }
}
```