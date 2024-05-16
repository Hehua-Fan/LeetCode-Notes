# LeetCode 1. Two Sum
## 题目链接
* [LeetCode 1. Two Sum](https://leetcode.cn/problems/two-sum/description/?envType=study-plan-v2&envId=top-100-liked)

## 题目大意
Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have **exactly one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

Example 1:
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```
Example 2:
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

## 解题思路
1.Sort + Two pointers(❌indices have changed)

2.Hashmap(key is num, value is index)

## 代码
### 思路1: Sort + Two pointers(❌indices have changed)
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        nums.sort()
        l = 0
        r = len(nums) - 1

        while l < r:
            sum = nums[l] + nums[r]
            if sum > target:
                r -= 1
            elif sum < target:
                l += 1
            else:
                return [l,r]

        return []

```
* Time Complexity: $O(n)$, where $n$ is the number of elements in the list `nums`
* Space Complexity: $O(1)$

### 思路2: Hashmap
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hash = {}

        for i, num in enumerate(nums):
            if target - num not in hash:
                hash[num] = i
            else:
                return [i, hash[target - num]]
```
* Time Complexity: $O(n)$, where $n$ is the number of elements in the list `nums`
* Space Complexity: $O(n)$, related to the auxiliary hash map.