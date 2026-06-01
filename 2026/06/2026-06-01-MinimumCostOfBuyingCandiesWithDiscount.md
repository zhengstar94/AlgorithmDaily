**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "2144. Minimum Cost of Buying Candies With Discount"
date: "2026-06-01"
tags: Easy
categories:
  - "LeetCode Greedy"
---


- A shop is selling candies at a discount. For **every two** candies sold, the shop gives a **third** candy for **free**.

- The customer can choose **any** candy to take away for free as long as the cost of the chosen candy is less than or equal to the **minimum** cost of the two candies bought.

  - For example, if there are `4` candies with costs `1`, `2`, `3`, and `4`, and the customer buys candies with costs `2` and `3`, they can take the candy with cost `1` for free, but not the candy with cost `4`.

- Given a **0-indexed** integer array `cost`, where `cost[i]` denotes the cost of the `ith` candy, return *the **minimum cost** of buying **all** the candies*.



**Example 1**

```
Input: cost = [1,2,3]
Output: 5
Explanation: We buy the candies with costs 2 and 3, and take the candy with cost 1 for free.
The total cost of buying all candies is 2 + 3 = 5. This is the only way we can buy the candies.
Note that we cannot buy candies with costs 1 and 3, and then take the candy with cost 2 for free.
The cost of the free candy has to be less than or equal to the minimum cost of the purchased candies.
```

**Example 2**

```
Input: cost = [6,5,7,9,2,2]
Output: 23
Explanation: The way in which we can get the minimum cost is described below:
- Buy candies with costs 9 and 7
- Take the candy with cost 6 for free
- We buy candies with costs 5 and 2
- Take the last remaining candy with cost 2 for free
Hence, the minimum cost to buy all candies is 9 + 7 + 5 + 2 = 23.
```

**Example 3**

```
Input: cost = [5,5]
Output: 10
Explanation: Since there are only 2 candies, we buy both of them. There is not a third candy we can take for free.
Hence, the minimum cost to buy all candies is 5 + 5 = 10.
```

## Method 1

```tex
【O(nlogn) time | O(logn) space】
```

```java
package Leetcode.Greedy;

import java.util.Arrays;

/**
 * @Author zhengxingxing
 * @Date 2026/06/01
 */
public class MinimumCostOfBuyingCandiesWithDiscount {

    public static int minimumCost(int[] cost) {

        // Sort the array in ascending order.
        // We will later traverse from right to left,
        // effectively processing candies in descending order.
        Arrays.sort(cost);

        // Stores the final minimum cost.
        int ans = 0;

        // Tracks the position within each group of three candies.
        //
        // count = 0 -> first candy in the group (must pay)
        // count = 1 -> second candy in the group (must pay)
        // count = 2 -> third candy in the group (free)
        int count = 0;

        // Traverse from the largest candy price to the smallest.
        for (int i = cost.length - 1; i >= 0; i--) {

            // Every third candy is obtained for free.
            // Skip adding its cost to the answer.
            if (count == 2) {
                count = 0; // Start a new group of three candies.
                continue;
            }

            // Add the candy price to the total cost
            // because this candy must be purchased.
            ans += cost[i];

            // Move to the next position within the current group.
            count++;
        }

        return ans;
    }

    public static void main(String[] args) {

        // Example 1:
        // Buy candies with prices 3 and 2,
        // get candy with price 1 for free.
        System.out.println(minimumCost(new int[]{1, 2, 3})); // 5

        // Example 2:
        // Buy 9 and 7, get 6 free.
        // Buy 5 and 2, get 2 free.
        System.out.println(minimumCost(new int[]{6, 5, 7, 9, 2, 2})); // 23

        // Example 3:
        // Only two candies exist, so both must be purchased.
        System.out.println(minimumCost(new int[]{5, 5})); // 10
    }
}
```