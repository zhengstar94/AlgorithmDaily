---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3005. Count Elements With Maximum Frequency"
date: "2025-09-22"
tags: Easy
categories:
  - "LeetCode HashTable"
---


- You are given an array `nums` consisting of **positive** integers.
- Return *the **total frequencies** of elements in* `nums` *such that those elements all have the **maximum** frequency*.
- The **frequency** of an element is the number of occurrences of that element in the array.

**Example 1**

```
Input: nums = [1,2,2,3,1,4]
Output: 4
Explanation: The elements 1 and 2 have a frequency of 2 which is the maximum frequency in the array.
So the number of elements in the array with maximum frequency is 4.
```

**Example 2**

```
Input: nums = [1,2,3,4,5]
Output: 5
Explanation: All elements of the array have a frequency of 1 which is the maximum.
So the number of elements in the array with maximum frequency is 5.
```

## Method 1

```tex
【O(n) time | O(n) space】
```

```java
package Leetcode.HashTable;

import java.util.HashMap;
import java.util.Map;

/**
 * @author zhengxingxing
 * @date 2025/09/22
 */
public class CountElementsWithMaximumFrequency {

    public static int maxFrequencyElements(int[] nums) {
        // Check if the input array is null or empty. If so, return 0.
        if (nums == null || nums.length == 0) {
            return 0;
        }

        // 1. Count the frequency of each element in the array.
        // Use a HashMap to store each element's frequency. Key: element, Value: frequency.
        Map<Integer, Integer> frequencyMap = new HashMap<>();

        // Iterate through the array and update the frequency of each element in the HashMap.
        for (int num : nums) {
            // For each element, increment its count in the frequencyMap.
            // If the element is not already in the map, put it with a default value of 0 and then increment.
            frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
        }

        // 2. Find the maximum frequency among all elements.
        int maxFrequency = 0;

        // Iterate through the values (frequencies) in the HashMap to find the maximum frequency.
        for (int frequency : frequencyMap.values()) {
            // Update maxFrequency if the current frequency is greater.
            maxFrequency = Math.max(maxFrequency, frequency);
        }

        // 3. Calculate the total frequency of elements that have the maximum frequency.
        int totalFrequency = 0;

        // Iterate through the keys (elements) in the HashMap.
        for (int num : frequencyMap.keySet()) {
            // Check if the frequency of the current element is equal to the maximum frequency.
            if (frequencyMap.get(num) == maxFrequency) {
                // If so, add its frequency to the total frequency.
                totalFrequency += frequencyMap.get(num);
            }
        }

        // Return the total frequency of elements with the maximum frequency.
        return totalFrequency;
    }

    /**
     * Main method to test the maxFrequencyElements method with sample test cases.
     *
     * @param args Command line arguments (not used).
     */
    public static void main(String[] args) {
        // Test Case 1
        int[] nums1 = {1, 2, 2, 3, 1, 4};
        int result1 = maxFrequencyElements(nums1);
        System.out.println("Result of Example 1: " + result1); // Output: 4

        // Test Case 2
        int[] nums2 = {1, 2, 3, 4, 5};
        int result2 = maxFrequencyElements(nums2);
        System.out.println("Result of Example 2: " + result2); // Output: 5
    }
}

```





