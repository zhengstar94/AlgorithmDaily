---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "1935. Maximum Number of Words You Can Type"
date: "2025-09-15"
tags: Easy
categories:
  - "LeetCode HashTable"
---∂

- There is a malfunctioning keyboard where some letter keys do not work. All other keys on the keyboard work properly.
- Given a string `text` of words separated by a single space (no leading or trailing spaces) and a string `brokenLetters` of all **distinct** letter keys that are broken, return *the **number of words** in* `text` *you can fully type using this keyboard*.

**Example 1**

```
Input: text = "hello world", brokenLetters = "ad"
Output: 1
Explanation: We cannot type "world" because the 'd' key is broken.
```

**Example 2**

```
Input: text = "leet code", brokenLetters = "lt"
Output: 1
Explanation: We cannot type "leet" because the 'l' and 't' keys are broken.
```

**Example 3**

```
Input: text = "leet code", brokenLetters = "e"
Output: 0
Explanation: We cannot type either word because the 'e' key is broken.
```

## Method 1

```tex
【O(n + m) time | O(n + m) space】
```

```java
package Leetcode.HashTable;

import java.util.HashSet;
import java.util.Set;

/**
 * @Author zhengxingxing
 * @Date 2025/09/15
 */
public class MaximumNumberOfWordsYouCanType {

    public static int canBeTypedWords(String text, String brokenLetters) {
        // Create a set to store all broken letters for O(1) lookup.
        Set<Character> broken = new HashSet<>();
        // Add each broken letter to the set.
        for (char c : brokenLetters.toCharArray()) {
            broken.add(c);
        }

        // Split the input text into individual words using space as the delimiter.
        String[] words = text.split(" ");
        int count = 0; // Initialize the counter for typable words.

        // Iterate through each word in the text.
        for (String word : words) {
            boolean canType = true; // Assume the word can be typed.

            // Check each character in the current word.
            for (char c : word.toCharArray()) {
                // If the character is in the broken set, this word cannot be typed.
                if (broken.contains(c)) {
                    canType = false; // Mark as untypable.
                    break; // No need to check the rest of the characters in this word.
                }
            }

            // If the word does not contain any broken letters, increment the counter.
            if (canType){
                count++;
            }
        }
        // Return the total number of typable words.
        return count;
    }

    public static void main(String[] args) {
        // Example 1: Only "hello" can be typed, "world" contains 'd' which is broken.
        System.out.println(canBeTypedWords("hello world", "ad")); // Output: 1

        // Example 2: Only "code" can be typed, "leet" contains 'l' and 't' which are broken.
        System.out.println(canBeTypedWords("leet code", "lt"));   // Output: 1

        // Example 3: Both words contain 'e', which is broken, so none can be typed.
        System.out.println(canBeTypedWords("leet code", "e"));    // Output: 0

        // Example 4: No broken letters, so all words can be typed.
        System.out.println(canBeTypedWords("a b c", ""));         // Output: 3

        // Example 5: All letters are broken, so none of the words can be typed.
        System.out.println(canBeTypedWords("a b c", "abc"));      // Output: 0
    }
}

```





