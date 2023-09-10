# ARTS Week 4

## Algorithm

```java
/**
222. Count Complete Tree Nodes

Given the root of a complete binary tree, return the number of the nodes in the tree.
According to Wikipedia, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. 
It can have between 1 and 2h nodes inclusive at the last level h.
Design an algorithm that runs in less than O(n) time complexity.

Example 1:
Input: root = [1,2,3,4,5,6]
Output: 6

Example 2:
Input: root = []
Output: 0

Example 3:
Input: root = [1]
Output: 1
*/

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */

// 暴力拆解
class Solution {
    public int countNodes(TreeNode root) {
        if (root == null) return 0;
        int left = countNodes(root.left);
    	int right = countNodes(root.right);
    	return left + right + 1;
    }
}
```

```java
// 完全二叉树解法
class Solution {
    public int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int level = 0;
        TreeNode node = root;
        while (node.left != null) {
            level++;
            node = node.left;
        }
        int low = 1 << level, high = (1 << (level + 1)) - 1;
        while (low < high) {
            int mid = (high - low + 1) / 2 + low;
            if (exists(root, level, mid)) {
                low = mid;
            } else {
                high = mid - 1;
            }
        }
        return low;
    }

    public boolean exists(TreeNode root, int level, int k) {
        int bits = 1 << (level - 1);
        TreeNode node = root;
        while (node != null && bits > 0) {
            if ((bits & k) == 0) {
                node = node.left;
            } else {
                node = node.right;
            }
            bits >>= 1;
        }
        return node != null;
    }
}
```

## Review

Github 上编程语言和代码质量的大规模研究。

有人从 GitHub 上分析了728 个项目、6300 万个 SLOC、29,000 位作者、150 万次提交、17 种语言。来证明编程语言对软件质量有什么影响。

https://cacm.acm.org/magazines/2017/10/221326-a-large-scale-study-of-programming-languages-and-code-quality-in-github/fulltext

## Technique/Tips

AI学习相关思维导图：

Artificial Intelligence (AI): Philosophy Mind Map

https://gogeometry.com/software/ai/artificial-intelligence-mind-map-philosophy.html

## Share

机器学习工程师需要了解的 10 种算法

来自：https://www.kdnuggets.com/2016/08/10-algorithms-machine-learning-engineers.html

- Decision Trees
- Naive Bayes Classification
- Ordinary Least Squares Regression
- Logistic Regression
- Support Vector Machines
- Ensemble Methods
- Clustering Algorithms
- Principal Component Analysis
- Singular Value Decomposition
- Independent Component Analysis
