---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3516. Find Closest Person"
date: "2025-09-05"
tags: Easy
categories:
  - "LeetCode Math"
---


- You are given three integers `x`, `y`, and `z`, representing the positions of three people on a number line:
  - `x` is the position of Person 1.
  - `y` is the position of Person 2.
  - `z` is the position of Person 3, who does **not** move.
- Both Person 1 and Person 2 move toward Person 3 at the **same** speed.
- Determine which person reaches Person 3 **first**:
  - Return 1 if Person 1 arrives first.
  - Return 2 if Person 2 arrives first.
  - Return 0 if both arrive at the **same** time.
- Return the result accordingly.

**Example 1**

```
Input: x = 2, y = 7, z = 4

Output: 1

Explanation:

- Person 1 is at position 2 and can reach Person 3 (at position 4) in 2 steps.
- Person 2 is at position 7 and can reach Person 3 in 3 steps.
Since Person 1 reaches Person 3 first, the output is 1.
```

**Example 2**

```
Input: x = 2, y = 5, z = 6

Output: 2

Explanation:

- Person 1 is at position 2 and can reach Person 3 (at position 6) in 4 steps.
- Person 2 is at position 5 and can reach Person 3 in 1 step.
Since Person 2 reaches Person 3 first, the output is 2.
```

**Example 2**

```
Input: x = 1, y = 5, z = 3

Output: 0

Explanation:

- Person 1 is at position 1 and can reach Person 3 (at position 3) in 2 steps.
- Person 2 is at position 5 and can reach Person 3 in 2 steps.
Since both Person 1 and Person 2 reach Person 3 at the same time, the output is 0.
```

## Method 1

```tex
【O(1) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/09/05
 */
public class FindClosestPerson {

    public static int findClosestPerson(int x, int y, int z) {
        int distance1 = Math.abs(x - z); // Distance from Person 1 to Person 3
        int distance2 = Math.abs(y - z); // Distance from Person 2 to Person 3

        if (distance1 < distance2) {
            return 1; // Person 1 arrives first
        } else if (distance2 < distance1) {
            return 2; // Person 2 arrives first
        } else {
            return 0; // They arrive at the same time
        }
    }

    public static void main(String[] args) {
        // Test cases
        System.out.println("Test Case 1: x=2, y=7, z=4  ->  " + findClosestPerson(2, 7, 4)); // Output 1
        System.out.println("Test Case 2: x=2, y=5, z=6  ->  " + findClosestPerson(2, 5, 6)); // Output 2
        System.out.println("Test Case 3: x=1, y=5, z=3  ->  " + findClosestPerson(1, 5, 3)); // Output 0
        System.out.println("Test Case 4: x=0, y=0, z=0  ->  " + findClosestPerson(0, 0, 0)); // Output 0
        System.out.println("Test Case 5: x=-1, y=1, z=0 ->  " + findClosestPerson(-1, 1, 0)); // Output 0
    }
}

```





