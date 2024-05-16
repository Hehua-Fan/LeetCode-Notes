# LeetCode 15. Three Sum
## 题目链接
* [LeetCode 15. Three Sum](https://leetcode.cn/problems/3sum/description/?envType=study-plan-v2&envId=top-100-liked)

## 题目大意
Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

 
Example 1:
```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
```

## 解题思路
Sort + Two pointers

**Important Code**

```python
# move to the next j, with the skip
j -= 1                                  
while i < j and nums[j] == nums[j+1]: j -= 1

# move to the next i, with the skip
i += 1
while i < j and nums[i] == nums[i-1]: i += 1

# move to the next (i,j), with the skip
i += 1
j -= 1
while i < j and nums[i] == nums[i - 1]: i += 1
while i < j and nums[j] == nums[j + 1]: j -= 1
```

## 代码
```python
class Solution:
    def threeSum(self, nums: [int]) -> [[int]]:
        nums.sort()
        k = 0
        n = len(nums)
        res = []

        for k in range(n - 2):                          # remain k as contraint temporarily
            if nums[k] > 0: break                       # nums[k] must < 0
            if k > 0 and nums[k] == nums[k-1]: continue # skip the same element for k
            i = k + 1
            j = n - 1
            while i < j:                                # two pointers
                if nums[k] + nums[i] + nums[j] > 0:
                    # move to the next j, with the skip
                    j -= 1                                  
                    while i < j and nums[j] == nums[j+1]: j -= 1
                elif nums[k] + nums[i] + nums[j] < 0:
                    # move to the next i, with the skip
                    i += 1
                    while i < j and nums[i] == nums[i-1]: i += 1
                else:
                    res.append([nums[k], nums[i], nums[j]])

                    # move to the next (i,j), with the skip
                    i += 1
                    j -= 1
                    while i < j and nums[i] == nums[i - 1]: i += 1
                    while i < j and nums[j] == nums[j + 1]: j -= 1
            
        return res
```
* Time Complexity: $O(n^2)$, for + while
* Space Complexity: $O(1)$
