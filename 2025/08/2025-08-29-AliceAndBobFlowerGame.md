---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3021. Alice and Bob Playing Flower Game"
date: "2025-08-29"
tags: Medium
categories:
  - "LeetCode Math"
---


- Alice and Bob are playing a turn-based game on a field, with two lanes of flowers between them. There are `x` flowers in the first lane between Alice and Bob, and `y` flowers in the second lane between them.
- The game proceeds as follows:
  1. Alice takes the first turn.
  2. In each turn, a player must choose either one of the lane and pick one flower from that side.
  3. At the end of the turn, if there are no flowers left at all, the **current** player captures their opponent and wins the game.
- Given two integers, `n` and `m`, the task is to compute the number of possible pairs `(x, y)` that satisfy the conditions:
  - Alice must win the game according to the described rules.
  - The number of flowers `x` in the first lane must be in the range `[1,n]`.
  - The number of flowers `y` in the second lane must be in the range `[1,m]`.
- Return *the number of possible pairs* `(x, y)` *that satisfy the conditions mentioned in the statement*.

**Example 1**

```
Input: n = 3, m = 2
Output: 3
Explanation: The following pairs satisfy conditions described in the statement: (1,2), (3,2), (2,1).
```

**Example 2**

```
Input: n = 1, m = 1
Output: 0
Explanation: No pairs satisfy the conditions described in the statement.
```

## Method 1

```tex
【O(1) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/08/29
 */
public class AliceAndBobFlowerGame {
    
    public static long flowerGame(int n, int m) {
        // Calculate the total number of (x, y) pairs and divide by 2 to get the number of pairs with an odd sum.
        return (long) n * m / 2;
    }

    public static void main(String[] args) {
        // Test cases to verify the solution

        // Example 1: n = 3, m = 2
        // Possible pairs: (1,1),(1,2),(2,1),(2,2),(3,1),(3,2)
        // Alice wins for (1,2), (2,1), (3,2) => Output: 3
        System.out.println(flowerGame(3, 2)); // Output: 3

        // Example 2: n = 1, m = 1
        // Only one pair: (1,1), sum is even => Output: 0
        System.out.println(flowerGame(1, 1)); // Output: 0

        // Example 3: n = 5, m = 4
        // Total pairs: 20, Alice wins in 10 cases
        System.out.println(flowerGame(5, 4)); // Output: 10

        // Example 4: n = 10, m = 10
        // Total pairs: 100, Alice wins in 50 cases
        System.out.println(flowerGame(10, 10)); // Output: 50
    }
}

```





