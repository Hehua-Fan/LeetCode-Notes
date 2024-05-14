# 剑指Offer03.数组中重复的数字
## 题目链接
* [剑指 Offer 03. 数组中重复的数字 - 力扣](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

## 题目大意
给定一个包含 n + 1 个整数的数组 nums，里边包含的值都在 1 ~ n 之间。假设 nums 中只存在一个重复的整数，要求找出这个重复的数。

## 解题思路
使用哈希表存储数组每个元素，遇到重复元素则直接返回该元素。

## 代码
```python
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        nums_dict = dict()
        for num in nums:
            if num in nums_dict:
                return num
            nums_dict[num] = 1
        return -1
```

* Time Complexity: $O(n)$, where $n$ is the number of elements in the list `nums`
* Space Complexity: $O(n)$, where $n$ is the number of elements in the list `nums`