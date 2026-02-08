---
toc:
  beginning: true
giscus_comments: true
layout: post
title: "110. Balanced Binary Tree"
date: "2026-02-08"
tags: Easy
categories:
  - "LeetCode Trees"
---


- Given a binary tree, determine if it is **height-balanced**.

**Example 1**

```
Input: root = [3,9,20,null,null,15,7]
Output: true
```

**Example 2**

```
Input: root = [1,2,2,3,3,null,null,4,4]
Output: false
```

**Example 3**

```
Input: root = []
Output: true
```

## Method 1

```tex
【O(n) time | O(n) space】
```

```java
package Leetcode.Trees;

/**
 * @Author zhengxingxing
 * @Date 2026/02/08
 */
public class BalancedBinaryTree {

    public static boolean isBalanced(TreeNode root) {
        // If checkHeight returns -1, tree is unbalanced -> return false
        // If checkHeight returns any non-negative number, tree is balanced -> return true
        return checkHeight(root) != -1;
    }
    
    private static int checkHeight(TreeNode node) {
        // Base case: null node has height 0
        // This is the starting point for leaf nodes' parents
        if(node == null){
            return 0;
        }

        // Step 1: Recursively get left subtree height
        // This goes all the way down to leftmost leaf before returning
        int leftHeight = checkHeight(node.left);

        // Early termination (Pruning):
        // If left subtree is already unbalanced (returned -1),
        // no need to check right subtree or current node.
        // Propagate -1 up immediately to save computation time.
        if (leftHeight == -1){
            return -1;
        }

        // Step 2: Recursively get right subtree height
        // Only executes if left subtree was balanced
        int rightHeight = checkHeight(node.right);

        // Early termination (Pruning):
        // If right subtree is unbalanced, propagate -1 up immediately
        if (rightHeight == -1){
            return -1;
        }

        // Step 3: Check balance condition at current node
        // Definition of balanced: |leftHeight - rightHeight| <= 1
        // If difference > 1, this node makes the tree unbalanced
        if (Math.abs(leftHeight - rightHeight) > 1) {
            // Return sentinel -1 to indicate "unbalanced found at this node"
            // This -1 will bubble up through all parent calls
            return -1;
        }

        // Step 4: Current node is balanced, calculate and return its height
        // Height of current node = max(height of left, height of right) + 1 (for current level)
        // The +1 accounts for the edge connecting current node to its child
        return Math.max(leftHeight, rightHeight) + 1;
    }

    
    public static void main(String[] args) {
        // ==================== Test Case 1 ====================
        // Input: [3,9,20,null,null,15,7] -> Expected: true
        // Tree Structure:
        //        3
        //       / \
        //      9  20
        //        /  \
        //       15   7
        //
        // Heights: 9(1), 15(1), 7(1), 20(2), 3(3)
        // Balance checks:
        // - Node 9: |0-0|=0 <= 1 ✓
        // - Node 20: |1-1|=0 <= 1 ✓
        // - Node 3: |1-2|=1 <= 1 ✓
        TreeNode root1 = new TreeNode(3);
        root1.left = new TreeNode(9);
        root1.right = new TreeNode(20);
        root1.right.left = new TreeNode(15);
        root1.right.right = new TreeNode(7);

        System.out.println("Test 1 (Expected: true): " + isBalanced(root1));

        // ==================== Test Case 2 ====================
        // Input: [1,2,2,3,3,null,null,4,4] -> Expected: false
        // Tree Structure:
        //           1
        //          / \
        //         2   2
        //        / \
        //       3   3
        //      / \
        //     4   4
        //
        // Heights:
        // - Left 4: 1, Right 4: 1 -> their parent 3: 2
        // - Left 3 (with 4s): 2, Right 3 (leaf): 1 -> their parent 2: 3
        // - Left 2: 3, Right 2 (leaf): 1 -> Root 1: |3-1|=2 > 1 UNBALANCED!
        // checkHeight will return -1 at root, so isBalanced returns false
        TreeNode root2 = new TreeNode(1);
        root2.left = new TreeNode(2);
        root2.right = new TreeNode(2);
        root2.left.left = new TreeNode(3);
        root2.left.right = new TreeNode(3);
        root2.left.left.left = new TreeNode(4);
        root2.left.left.right = new TreeNode(4);

        System.out.println("Test 2 (Expected: false): " + isBalanced(root2));

        // ==================== Edge Case ====================
        // Empty tree is considered balanced
        System.out.println("Test 3 - Empty tree (Expected: true): " + isBalanced(null));
    }
}
```