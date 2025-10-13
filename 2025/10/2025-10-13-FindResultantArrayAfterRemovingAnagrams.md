---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "2273. Find Resultant Array After Removing Anagrams"
date: "2025-10-13"
tags: Easy
categories:
  - "LeetCode Array"
---


- You are given a **0-indexed** string array `words`, where `words[i]` consists of lowercase English letters.
- In one operation, select any index `i` such that `0 < i < words.length` and `words[i - 1]` and `words[i]` are **anagrams**, and **delete** `words[i]` from `words`. Keep performing this operation as long as you can select an index that satisfies the conditions.
- Return `words` *after performing all operations*. It can be shown that selecting the indices for each operation in **any** arbitrary order will lead to the same result.
- An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase using all the original letters exactly once. For example, `"dacb"` is an anagram of `"abdc"`.

**Example 1**

```
Input: words = ["abba","baba","bbaa","cd","cd"]
Output: ["abba","cd"]
Explanation:
One of the ways we can obtain the resultant array is by using the following operations:
- Since words[2] = "bbaa" and words[1] = "baba" are anagrams, we choose index 2 and delete words[2].
  Now words = ["abba","baba","cd","cd"].
- Since words[1] = "baba" and words[0] = "abba" are anagrams, we choose index 1 and delete words[1].
  Now words = ["abba","cd","cd"].
- Since words[2] = "cd" and words[1] = "cd" are anagrams, we choose index 2 and delete words[2].
  Now words = ["abba","cd"].
We can no longer perform any operations, so ["abba","cd"] is the final answer.
```

**Example 2**

```
Input: words = ["a","b","c","d","e"]
Output: ["a","b","c","d","e"]
Explanation:
No two adjacent strings in words are anagrams of each other, so no operations are performed.
```

## Method 1

```tex
【O(N * K log K) time | O(N*K) space】
```

```java
package Array;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

/**
 * @Author zhengxingxing
 * @Date 2025/10/13
 */
public class FindResultantArrayAfterRemovingAnagrams {


    public static List<String> removeAnagrams(String[] words) {
        List<String> result = new ArrayList<>(); // Initialize a list to store the result.
        String prev = null; // Store the sorted form of the previous non-anagram word.

        for (String word : words) { // Iterate through the input array.
            char[] chars = word.toCharArray(); // Convert the word to a character array.
            Arrays.sort(chars); // Sort the character array to identify anagrams.
            String sortedWord = new String(chars); // Convert the sorted character array back to a string.

            if (prev == null || !sortedWord.equals(prev)) { // Check if the current word is an anagram of the previous word.
                result.add(word); // If not an anagram, add the original word to the result list.
                prev = sortedWord; // Update prev with the sorted form of the current word.
            }
        }
        return result; // Return the list with adjacent anagrams removed.
    }


    public static void main(String[] args) {
        String[] words1 = {"abba", "baba", "bbaa", "cd", "cd"};
        System.out.println("Input: " + Arrays.toString(words1));
        System.out.println("Output: " + removeAnagrams(words1)); // Output: [abba, cd]

        String[] words2 = {"a", "b", "c", "d", "e"};
        System.out.println("Input: " + Arrays.toString(words2));
        System.out.println("Output: " + removeAnagrams(words2)); // Output: [a, b, c, d, e]
    }
}

```





