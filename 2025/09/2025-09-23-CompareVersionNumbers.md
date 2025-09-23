---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "165. Compare Version Numbers"
date: "2025-09-23"
tags: Medium
categories:
  - "LeetCode Math"
---

- Given two **version strings**, `version1` and `version2`, compare them. A version string consists of **revisions** separated by dots `'.'`. The **value of the revision** is its **integer conversion** ignoring leading zeros.
- To compare version strings, compare their revision values in **left-to-right order**. If one of the version strings has fewer revisions, treat the missing revision values as `0`.
- Return the following:
  - If `version1 < version2`, return -1.
  - If `version1 > version2`, return 1.
  - Otherwise, return 0.

**Example 1**

```
Input: version1 = "1.2", version2 = "1.10"

Output: -1

Explanation:

version1's second revision is "2" and version2's second revision is "10": 2 < 10, so version1 < version2.
```

**Example 2**

```
Input: version1 = "1.01", version2 = "1.001"

Output: 0

Explanation:

Ignoring leading zeroes, both "01" and "001" represent the same integer "1".
```

**Example 3**

```
Input: version1 = "1.0", version2 = "1.0.0.0"

Output: 0

Explanation:

version1 has less revisions, which means every missing revision are treated as "0".
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Math;

/**
 * @Author zhengxingxing
 * @Date 2025/09/23
 */
public class CompareVersionNumbers {
    
    public static int compareVersion(String version1, String version2) {
        // Split the version strings by "."
        String[] v1 = version1.split("\\.");
        String[] v2 = version2.split("\\.");

        // Determine the maximum length between the two version number arrays
        int maxLength = Math.max(v1.length, v2.length);

        // Iterate through the revisions and compare them
        for (int i = 0; i < maxLength; i++) {
            // Parse the revision at the current index, or default to 0 if the index is out of bounds
            int num1 = (i < v1.length) ? Integer.parseInt(v1[i]) : 0;
            int num2 = (i < v2.length) ? Integer.parseInt(v2[i]) : 0;

            // Compare the integer values of the revisions
            if (num1 < num2) {
                return -1; // version1 is less than version2
            } else if (num1 > num2) {
                return 1;  // version1 is greater than version2
            }
            // If num1 == num2, continue to the next revision
        }

        // If all revisions are equal, the version numbers are equal
        return 0;
    }

    public static void main(String[] args) {
        // Test cases
        System.out.println("1.2 vs 1.10: " + compareVersion("1.2", "1.10"));   // Output: -1
        System.out.println("1.01 vs 1.001: " + compareVersion("1.01", "1.001")); // Output: 0
        System.out.println("1.0 vs 1.0.0.0: " + compareVersion("1.0", "1.0.0.0")); // Output: 0
        System.out.println("0.1 vs 1.1: " + compareVersion("0.1", "1.1"));    // Output: -1
    }
}

```





