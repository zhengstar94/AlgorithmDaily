---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "2169. Count Operations to Obtain Zero"
date: "2025-11-09"
tags: Easy
categories:
  - "LeetCode Math"
---

- You are given two **non-negative** integers `num1` and `num2`.

- In one **operation**, if `num1 >= num2`, you must subtract `num2` from `num1`, otherwise subtract `num1` from `num2`.

  - For example, if `num1 = 5` and `num2 = 4`, subtract `num2` from `num1`, thus obtaining `num1 = 1` and `num2 = 4`. However, if `num1 = 4` and `num2 = 5`, after one operation, `num1 = 4` and `num2 = 1`.

- Return *the **number of operations** required to make either* `num1 = 0` *or* `num2 = 0`.



**Example 1**

```
Input: num1 = 2, num2 = 3
Output: 3
Explanation: 
- Operation 1: num1 = 2, num2 = 3. Since num1 < num2, we subtract num1 from num2 and get num1 = 2, num2 = 3 - 2 = 1.
- Operation 2: num1 = 2, num2 = 1. Since num1 > num2, we subtract num2 from num1.
- Operation 3: num1 = 1, num2 = 1. Since num1 == num2, we subtract num2 from num1.
Now num1 = 0 and num2 = 1. Since num1 == 0, we do not need to perform any further operations.
So the total number of operations required is 3.
```

**Example 2**

```
Input: num1 = 10, num2 = 10
Output: 1
Explanation: 
- Operation 1: num1 = 10, num2 = 10. Since num1 == num2, we subtract num2 from num1 and get num1 = 10 - 10 = 0.
Now num1 = 0 and num2 = 10. Since num1 == 0, we are done.
So the total number of operations required is 1.
```

## Method 1

```tex
【O(max(num1, num2)) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/11/09  
 */
public class CountOperationsToObtainZero {

    public static int countOperations(int num1, int num2) {
        int operations = 0; // Initialize the operation counter

        // Continue the loop as long as both num1 and num2 are not zero
        while (num1 != 0 && num2 != 0) {
            // If num1 is greater than or equal to num2, subtract num2 from num1
            if (num1 >= num2) {
                num1 -= num2;
            } else {
                // Otherwise, subtract num1 from num2
                num2 -= num1;
            }

            operations++; // Increment the operation counter
        }

        return operations; // Return the total number of operations performed
    }

    public static void main(String[] args) {
        // Test case 1
        int num1 = 2;
        int num2 = 3;
        int result1 = countOperations(num1, num2);
        System.out.println("Input: num1 = " + num1 + ", num2 = " + num2 + ", Output: " + result1); // Output: 3

        // Test case 2
        num1 = 10;
        num2 = 10;
        int result2 = countOperations(num1, num2);
        System.out.println("Input: num1 = " + num1 + ", num2 = " + num2 + ", Output: " + result2); // Output: 1
    }
}

```





