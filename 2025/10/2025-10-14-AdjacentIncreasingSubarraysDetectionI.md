---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3349. Adjacent Increasing Subarrays Detection I"
date: "2025-10-14"
tags: Easy
categories:
  - "LeetCode Array"
---

- Given an array `nums` of `n` integers and an integer `k`, determine whether there exist **two** **adjacent** subarrays of length `k` such that both subarrays are **strictly** **increasing**. Specifically, check if there are **two** subarrays starting at indices `a` and `b` (`a < b`), where:
  - Both subarrays `nums[a..a + k - 1]` and `nums[b..b + k - 1]` are **strictly increasing**.
  - The subarrays must be **adjacent**, meaning `b = a + k`.
- Return `true` if it is *possible* to find **two** such subarrays, and `false` otherwise.

**Example 1**

```
Input: nums = [2,5,7,8,9,2,3,4,3,1], k = 3

Output: true

Explanation:

The subarray starting at index 2 is [7, 8, 9], which is strictly increasing.
The subarray starting at index 5 is [2, 3, 4], which is also strictly increasing.
These two subarrays are adjacent, so the result is true.
```

**Example 2**

```
Input: nums = [1,2,3,4,4,4,4,5,6,7], k = 5

Output: false
```

## Method 1

```tex
【O((N - 2K) * K) time | O(1) space】
```

```java
package Array;

import java.util.ArrayList;
import java.util.List;

/**
 * @Author zhengxingxing
 * @Date 2025/10/14
 */
public class AdjacentIncreasingSubarraysDetectionI {
    
    public static boolean hasIncreasingSubarrays(List<Integer> nums, int k) {
        // Check for edge cases: If the input list is null, the list size is less than twice 'k' (making it impossible to have two adjacent subarrays of length 'k'), or 'k' is non-positive, return false.
        if (nums == null || nums.size() < 2 * k || k <= 0) {
            return false; // Handle edge cases: null list, list too short to contain two adjacent subarrays of length k, or invalid k value.
        }

        // Iterate through possible starting indices 'a' of the first subarray.  The loop continues as long as 'a' can be a valid starting index for the first subarray,
        // while also ensuring there's enough space for the second adjacent subarray of length 'k'. Specifically, 'a' can range from 0 to nums.size() - 2*k (inclusive).
        for (int a = 0; a <= nums.size() - 2 * k; a++) {
            // Calculate the starting index 'b' of the second subarray. Since the subarrays must be adjacent, 'b' is always 'a + k'.
            int b = a + k; // Subarrays must be adjacent, meaning b = a + k.

            // Check if both the subarray starting at index 'a' and the subarray starting at index 'b' are strictly increasing, by calling the helper method isStrictlyIncreasing().
            // If both subarrays are strictly increasing, it means we've found the pair of adjacent increasing subarrays we were looking for, so we return true.
            if (isStrictlyIncreasing(nums, a, k) && isStrictlyIncreasing(nums, b, k)) {
                return true; // Found two adjacent strictly increasing subarrays.
            }
        }

        // If the loop completes without finding any pair of adjacent strictly increasing subarrays, it means no such subarrays exist within the input list, so we return false.
        return false; // No such subarrays found.
    }
    
    private static boolean isStrictlyIncreasing(List<Integer> nums, int start, int k) {
        // Iterate through the elements of the subarray from 'start' to 'start + k - 1'.
        for (int i = start; i < start + k - 1; i++) {
            // Check if the current element is greater than or equal to the next element.  If it is, it means the subarray is not strictly increasing.
            // Note that nums.get(i) retrieves the element at index 'i' within the list.
            if (nums.get(i) >= nums.get(i + 1)) {
                return false; // Found a pair of elements that are not strictly increasing, so the subarray is not strictly increasing.
            }
        }

        // If the inner loop completes without finding any pair of elements that violate the strictly increasing order, it means the subarray is strictly increasing, so we return true.
        return true; // All elements are strictly increasing, so the subarray is strictly increasing.
    }

    public static void main(String[] args) {
        // Test cases
        List<Integer> nums1 = new ArrayList<>();
        nums1.add(2); nums1.add(5); nums1.add(7); nums1.add(8); nums1.add(9); nums1.add(2); nums1.add(3); nums1.add(4); nums1.add(3); nums1.add(1);
        int k1 = 3;
        System.out.println("Input: nums = " + nums1 + ", k = " + k1);
        System.out.println("Output: " + hasIncreasingSubarrays(nums1, k1));

        List<Integer> nums2 = new ArrayList<>();
        nums2.add(1); nums2.add(2); nums2.add(3); nums2.add(4); nums2.add(4); nums2.add(4); nums2.add(4); nums2.add(5); nums2.add(6); nums2.add(7);
        int k2 = 5;
        System.out.println("Input: nums = " + nums2 + ", k = " + k2);
        System.out.println("Output: " + hasIncreasingSubarrays(nums2, k2));
    }
}
```





