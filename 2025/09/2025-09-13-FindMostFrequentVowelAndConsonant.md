---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3541. Find Most Frequent Vowel and Consonant"
date: "2025-09-13"
tags: Easy
categories:
  - "LeetCode Array"
---


- You are given a string `s` consisting of lowercase English letters (`'a'` to `'z'`).
- Your task is to:
  - Find the vowel (one of `'a'`, `'e'`, `'i'`, `'o'`, or `'u'`) with the **maximum** frequency.
  - Find the consonant (all other letters excluding vowels) with the **maximum** frequency.
- Return the sum of the two frequencies.
- **Note**: If multiple vowels or consonants have the same maximum frequency, you may choose any one of them. If there are no vowels or no consonants in the string, consider their frequency as 0.
- The **frequency** of a letter `x` is the number of times it occurs in the string.

**Example 1**

```
Input: s = "successes"
Output: 6
Explanation:

The vowels are: 'u' (frequency 1), 'e' (frequency 2). The maximum frequency is 2.
The consonants are: 's' (frequency 4), 'c' (frequency 2). The maximum frequency is 4.
The output is 2 + 4 = 6.
```

**Example 2**

```
Input: s = "aeiaeia"
Output: 3

Explanation:

The vowels are: 'a' (frequency 3), 'e' ( frequency 2), 'i' (frequency 2). The maximum frequency is 3.
There are no consonants in s. Hence, maximum consonant frequency = 0.
The output is 3 + 0 = 3.
```

## Method 1

```tex
【O(n) time | O(n) space】
```

```java
package Leetcode.Array;

/**
 * @Author zhengxingxing
 * @Date 2025/09/13
 */
public class FindMostFrequentVowelAndConsonant {

    public static int maxVowelAndConsonantFreq(String s) {
        // Array to record the frequency of each letter (a-z).
        // freq[0] corresponds to 'a', freq[1] to 'b', ..., freq[25] to 'z'.
        int[] freq = new int[26];
        for (char c : s.toCharArray()) {
            freq[c - 'a']++;
        }

        // Boolean array to mark which letters are vowels.
        // isVowel[0] is true if 'a' is a vowel, etc.
        boolean[] isVowel = new boolean[26];
        for (char c : "aeiou".toCharArray()) {
            isVowel[c - 'a'] = true;
        }

        int maxVowel = 0, maxConsonant = 0;
        // Iterate through all 26 letters to find the max frequency for vowels and consonants.
        for (int i = 0; i < 26; i++) {
            if (freq[i] == 0) continue; // Skip letters that do not appear in the string.
            if (isVowel[i]) {
                // If the letter is a vowel, update maxVowel if this frequency is higher.
                maxVowel = Math.max(maxVowel, freq[i]);
            } else {
                // If the letter is a consonant, update maxConsonant if this frequency is higher.
                maxConsonant = Math.max(maxConsonant, freq[i]);
            }
        }
        // Return the sum of the highest vowel and consonant frequencies.
        return maxVowel + maxConsonant;
    }

    // Main method with test cases to verify the solution.
    public static void main(String[] args) {
        System.out.println(maxVowelAndConsonantFreq("successes")); // Output: 6
        System.out.println(maxVowelAndConsonantFreq("aeiaeia"));   // Output: 3
        System.out.println(maxVowelAndConsonantFreq("zzz"));       // Output: 3
        System.out.println(maxVowelAndConsonantFreq("aeiou"));     // Output: 1
        System.out.println(maxVowelAndConsonantFreq(""));          // Output: 0
    }
}

```





