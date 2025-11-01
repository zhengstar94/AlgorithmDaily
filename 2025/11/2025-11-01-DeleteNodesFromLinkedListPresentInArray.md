---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "3217. Delete Nodes From Linked List Present in Array"
date: "2025-11-01"
tags: Medium
categories:
  - "LeetCode LinkedList"
---

- You are given an array of integers `nums` and the `head` of a linked list. Return the `head` of the modified linked list after **removing** all nodes from the linked list that have a value that exists in `nums`.

**Example 1**

```
Input: nums = [1,2,3], head = [1,2,3,4,5]

Output: [4,5]

Explanation:
Remove the nodes with values 1, 2, and 3.
```

**Example 2**

```
Input: nums = [1], head = [1,2,1,2,1,2]

Output: [2,2,2]

Explanation:
Remove the nodes with value 1.
```

**Example 3**

```
Input: nums = [5], head = [1,2,3,4]

Output: [1,2,3,4]

Explanation:
No node has value 5.
```

## Method 1

```tex
【O(m + n) time | O(m) space】
```

```java
package Leetcode.LinkList;

import java.util.HashSet;
import java.util.Set;

/**
 * @Author zhengxingxing
 * @Date 2025/11/01
 */
public class DeleteNodesFromLinkedListPresentInArray {

    public static ListNode modifiedList(int[] nums, ListNode head) {
        // 1. Create a HashSet to store the node values that need to be deleted for efficient lookups.
        Set<Integer> deleteSet = new HashSet<>();
        for (int num : nums) {
            deleteSet.add(num);
        }
        // 2. Use a dummy node to simplify the logic for deleting the head node (if needed).
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode current = dummy;
        // 3. Iterate through the linked list using two pointers to delete nodes.
        while (current.next != null) {
            if (deleteSet.contains(current.next.val)) {
                // If the value of the next node needs to be deleted,
                // point the current node's next pointer to the node after the next node,
                // effectively removing the next node from the linked list.
                current.next = current.next.next;
            } else {
                // If the value of the next node does not need to be deleted,
                // move the current pointer to the next node.
                current = current.next;
            }
        }
        // 4. Return the head node of the modified linked list.
        return dummy.next;
    }

    public static void main(String[] args) {
        // Test case 1
        int[] nums1 = {1, 2, 3};
        ListNode head1 = new ListNode(1);
        head1.next = new ListNode(2);
        head1.next.next = new ListNode(3);
        head1.next.next.next = new ListNode(4);
        head1.next.next.next.next = new ListNode(5);
        ListNode result1 = modifiedList(nums1, head1);
        printLinkedList(result1); // Output: 4 -> 5 -> null
        // Test case 2
        int[] nums2 = {1};
        ListNode head2 = new ListNode(1);
        head2.next = new ListNode(2);
        head2.next.next = new ListNode(1);
        head2.next.next.next = new ListNode(2);
        head2.next.next.next.next = new ListNode(1);
        head2.next.next.next.next.next = new ListNode(2);
        ListNode result2 = modifiedList(nums2, head2);
        printLinkedList(result2); // Output: 2 -> 2 -> 2 -> null
        // Test case 3
        int[] nums3 = {5};
        ListNode head3 = new ListNode(1);
        head3.next = new ListNode(2);
        head3.next.next = new ListNode(3);
        head3.next.next.next = new ListNode(4);
        ListNode result3 = modifiedList(nums3, head3);
        printLinkedList(result3); // Output: 1 -> 2 -> 3 -> 4 -> null
    }
    
    private static void printLinkedList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " -> ");
            current = current.next;
        }
        System.out.println("null");
    }
}

```





