# LeetCode 101. Symmetric Tree
## 题目链接
* [LeetCode 101. Symmetric Tree](https://leetcode.cn/problems/symmetric-tree/description/?envType=study-plan-v2&envId=top-100-liked)

## 题目大意
Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

## 解题思路
递归：root.val相同，左子树等于右子树，右子树等于左子树

## 代码
```python
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        return self.isSame(root.left, root.right)
    def isSame(self, p, q):
        if p is None or q is None:
            return p is q
        return p.val == q.val and self.isSame(p.left, q.right) and self.isSame(p.right, q.left)
```
* Time Complexity: $O(n)$
* Space Complexity: $O(n)$, 最坏情况是，只有左子树（相当于链表），栈帧空间是$n$