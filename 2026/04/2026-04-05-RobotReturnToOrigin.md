**---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "657. Robot Return to Origin"
date: "2026-04-05"
tags: Easy
categories:
  - "LeetCode Math"
---

- There is a robot starting at the position `(0, 0)`, the origin, on a 2D plane. Given a sequence of its moves, judge if this robot **ends up at** `(0, 0)` after it completes its moves.
- You are given a string `moves` that represents the move sequence of the robot where `moves[i]` represents its `ith` move. Valid moves are `'R'` (right), `'L'` (left), `'U'` (up), and `'D'` (down).
- Return `true` *if the robot returns to the origin after it finishes all of its moves, or* `false` *otherwise*.
- **Note**: The way that the robot is "facing" is irrelevant. `'R'` will always make the robot move to the right once, `'L'` will always make it move left, etc. Also, assume that the magnitude of the robot's movement is the same for each move.

**Example 1**

```
Input: moves = "UD"
Output: true
Explanation: The robot moves up once, and then down once. All moves have the same magnitude, so it ended up at the origin where it started. Therefore, we return true.
```

**Example 2**

```
Input: moves = "LL"
Output: false
Explanation: The robot moves left twice. It ends up two "moves" to the left of the origin. We return false because it is not at the origin at the end of its moves.
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2026/04/05
 */
public class RobotReturnToOrigin {

    public static boolean judgeCircle(String moves) {
        // Initialize coordinates at the origin
        int x = 0;
        int y = 0;

        // Traverse each character in the move sequence
        // Using toCharArray() is slightly faster than charAt() traversal on some JVMs
        for (char move : moves.toCharArray()) {
            if (move == 'U') {
                y++; // Move up, Y-axis increases
            } else if (move == 'D') {
                y--; // Move down, Y-axis decreases
            } else if (move == 'L') {
                x--; // Move left, X-axis decreases
            } else if (move == 'R') {
                x++; // Move right, X-axis increases
            }
        }

        // Only when the displacement in both horizontal and vertical directions is offset to 0,
        // it indicates a return to the origin
        return x == 0 && y == 0;
    }

    public static void main(String[] args) {
        // Test case 1
        String moves1 = "UD";
        System.out.println("Input: \"" + moves1 + "\" -> Output: " + judgeCircle(moves1)); // Expected: true

        // Test case 2
        String moves2 = "LL";
        System.out.println("Input: \"" + moves2 + "\" -> Output: " + judgeCircle(moves2)); // Expected: false

        // Test case 3
        String moves3 = "RRDDLLUU";
        System.out.println("Input: \"" + moves3 + "\" -> Output: " + judgeCircle(moves3)); // Expected: true
    }
}
```