**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "2833. Furthest Point From Origin"
date: "2026-04-23"
tags: Easy
categories:
  - "LeetCode Greedy"
---


- You are given a string `moves` of length `n` consisting only of characters `'L'`, `'R'`, and `'_'`. The string represents your movement on a number line starting from the origin `0`.

- In the `ith` move, you can choose one of the following directions:

  - move to the left if `moves[i] = 'L'` or `moves[i] = '_'`
  - move to the right if `moves[i] = 'R'` or `moves[i] = '_'`

- Return *the **distance from the origin** of the **furthest** point you can get to after* `n` *moves*.




**Example 1**

```
Input: moves = "L_RL__R"
Output: 3
Explanation: The furthest point we can reach from the origin 0 is point -3 through the following sequence of moves "LLRLLLR".
```

**Example 2**

```
Input: moves = "_R__LL_"
Output: 5
Explanation: The furthest point we can reach from the origin 0 is point -5 through the following sequence of moves "LRLLLLL".
```

**Example 3**

```
Input: moves = "_______"
Output: 7
Explanation: The furthest point we can reach from the origin 0 is point 7 through the following sequence of moves "RRRRRRR".
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Greedy;

/**
 * @Author zhengxingxing
 * @Date 2026/04/24
 */
public class FurthestPointFromOrigin {
    
    public static int furthestDistanceFromOrigin(String moves) {
        int countL = 0; // Count of 'L' moves
        int countR = 0; // Count of 'R' moves
        int countUnderscore = 0; // Count of '_' moves (wildcards)

        // Iterate through the string to count each type of character
        for (char move : moves.toCharArray()) {
            if (move == 'L') {
                countL++;
            } else if (move == 'R') {
                countR++;
            } else {
                countUnderscore++;
            }
        }

        // The base distance is the absolute difference between left and right moves.
        // All wildcard moves ('_') are used to maximize this distance.
        return Math.abs(countL - countR) + countUnderscore;
    }
    
    public static void main(String[] args) {
        // Test Case 1
        String moves1 = "L_RL__R";
        int result1 = furthestDistanceFromOrigin(moves1);
        System.out.println("Input: \"" + moves1 + "\"");
        System.out.println("Output: " + result1); // Expected output: 3
        System.out.println("---");

        // Test Case 2
        String moves2 = "_R__LL_";
        int result2 = furthestDistanceFromOrigin(moves2);
        System.out.println("Input: \"" + moves2 + "\"");
        System.out.println("Output: " + result2); // Expected output: 5
        System.out.println("---");

        // Test Case 3
        String moves3 = "_______";
        int result3 = furthestDistanceFromOrigin(moves3);
        System.out.println("Input: \"" + moves3 + "\"");
        System.out.println("Output: " + result3); // Expected output: 7
        System.out.println("---");

        // Additional Test Case
        String moves4 = "RRR";
        int result4 = furthestDistanceFromOrigin(moves4);
        System.out.println("Input: \"" + moves4 + "\"");
        System.out.println("Output: " + result4); // Expected output: 3
        System.out.println("---");

        // Additional Test Case
        String moves5 = "LRLR";
        int result5 = furthestDistanceFromOrigin(moves5);
        System.out.println("Input: \"" + moves5 + "\"");
        System.out.println("Output: " + result5); // Expected output: 0
        System.out.println("---");
    }
}
```