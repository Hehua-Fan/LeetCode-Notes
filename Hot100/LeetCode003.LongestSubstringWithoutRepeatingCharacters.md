# LeetCode 3. Longest Substring Without Repeating Characters
## 题目链接
* [LeetCode 3. Longest Substring Without Repeating Characters](https://leetcode.cn/problems/longest-substring-without-repeating-characters/description/?envType=study-plan-v2&envId=top-100-liked)

## 题目大意
Given a string `s`, find the length of the **longest substring** without repeating characters.

Example 1:
```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```
Example 2:
```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

## 解题思路
sliding window

## 代码
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        window = Counter()
        left, right = 0, 0
        res = 0
        
        while right < len(s):             # 右侧窗口扩大
            c = s[right]
            right += 1
            window[c] += 1
            
            while window[c] > 1:          # 判断左侧窗口是否要收缩
                d = s[left]
                left += 1
                window[d] -= 1 
            res = max(res, right - left)    
        
        return res
```
* Time Complexity: $O(n)$, where $n$ is the number of elements in the list `nums`
* Space Complexity: $O(n)$, where $n$ is the number of elements in the list `nums`