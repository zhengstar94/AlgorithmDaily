---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1653. Minimum Deletions to Make String Balanced"
date: "2026-02-07"
tags: Medium
categories:
  - "LeetCode Greedy"
---



- You are given a string `s` consisting only of characters `'a'` and `'b'`.
- You can delete any number of characters in `s` to make `s` **balanced**. `s` is **balanced** if there is no pair of indices `(i,j)` such that `i < j` and `s[i] = 'b'` and `s[j]= 'a'`.
- Return *the **minimum** number of deletions needed to make* `s` ***balanced***.

**Example 1**

```
Input: s = "aababbab"
Output: 2
Explanation: You can either:
Delete the characters at 0-indexed positions 2 and 6 ("aababbab" -> "aaabbb"), or
Delete the characters at 0-indexed positions 3 and 6 ("aababbab" -> "aabbbb").
```

**Example 2**

```
Input: s = "bbaaaaabb"
Output: 2
Explanation: The only solution is to delete the first two characters.
```

## Method 1

```tex
【O(n) time | O(1) space】
```

```java
package Leetcode.Greedy;

/**
 * @Author zhengxingxing
 * @Date 2026/02/07
 */
public class MinimumDeletionsToMakeStringBalanced {
    
    public static int minimumDeletions(String s) {
        // Step 1: Count the total number of 'a's in the entire string
        // This represents the initial cost when dividing line is at leftmost position
        // (all 'a's are in suffix and need to be deleted)
        int totalA = 0;
        for (char c : s.toCharArray()) {
            if (c == 'a') {
                totalA++;
            }
        }

        // Step 2: Initialize state
        // deletions: current cost at current dividing line position
        // minDeletions: minimum cost found so far across all positions
        // Initial state: dividing line at leftmost, suffix contains all characters
        // Cost = delete all 'a's from suffix
        int deletions = totalA;
        int minDeletions = totalA;

        // Step 3: Traverse string from left to right, simulating dividing line moving rightward
        // Each iteration moves one character from suffix to prefix
        for (char c : s.toCharArray()) {
            if (c == 'a') {
                // Current character is 'a'
                // It moves from suffix to prefix, so it can be kept now
                // Reduction: no longer need to delete this 'a' from suffix
                // Cost decreases by 1
                deletions--;
            } else { // c == 'b'
                // Current character is 'b'
                // It moves from suffix to prefix, but prefix can only contain 'a's
                // This 'b' must be deleted from prefix
                // Cost increases by 1
                deletions++;
            }

            // Step 4: Update minimum cost after moving dividing line to current position
            // Track the smallest cost across all possible dividing line positions
            minDeletions = Math.min(minDeletions, deletions);
        }

        // Step 5: Return the minimum deletion cost found
        // This represents the optimal dividing line position
        return minDeletions;
    }
    
    public static void main(String[] args) {
        // Example 1: "aababbab"
        // Optimal division: "aa|babbab" or "aaba|bbab" -> delete 2 characters
        String s1 = "aababbab";
        System.out.println(s1 + " -> " + minimumDeletions(s1)); // Expected: 2

        // Example 2: "bbaaaaabb"
        // Optimal division: "|bbaaaaabb" -> delete first 2 'b's
        String s2 = "bbaaaaabb";
        System.out.println(s2 + " -> " + minimumDeletions(s2)); // Expected: 2
    }
}

```