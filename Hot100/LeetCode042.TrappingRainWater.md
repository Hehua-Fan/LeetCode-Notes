# LeetCode 42. Trapping Rain Water
## 题目链接
* [LeetCode 42. Trapping Rain Water](https://leetcode.cn/problems/trapping-rain-water/description/?envType=study-plan-v2&envId=top-100-liked)

## 题目大意
Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

Example 1:
```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```

## 解题思路
1.prefix sum

2.two pointers

## 代码
### 思路1: prefix sum
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        n = len(height)
        pre_max = [0] * n
        pre_max[0] = height[0]
        for i in range(1, n):
            pre_max[i] = max(pre_max[i-1], height[i])

        sur_max = [0] * n
        sur_max[-1] = height[-1]
        for i in range(n-2,-1,-1):
            sur_max[i] = max(sur_max[i+1], height[i])

        res = 0
        for i in range(n):
            res += min(pre_max[i], sur_max[i]) - height[i]

        return res
```
* Time Complexity: $O(n)$, where $n$ is the number of elements in the list `height`
* Space Complexity: $O(n)$

### 思路2: two pointers
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        n = len(height)
        left = 0
        right = n - 1
        pre_max = 0
        sur_max = 0
        res = 0

        while left < right:
            pre_max = max(height[left], pre_max)
            sur_max = max(height[right], sur_max)
            if pre_max < sur_max:
                res += pre_max - height[left]
                left += 1
            else:
                res += sur_max - height[right]
                right -= 1

        return res
```
* Time Complexity: $O(n)$, where $n$ is the number of elements in the list `height`
* Space Complexity: $O(1)$