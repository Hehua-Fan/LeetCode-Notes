
# LeetCode 215. Kth Largest Element in an Array
## 题目链接
* [LeetCode 215. Kth Largest Element in an Array](https://leetcode.cn/problems/kth-largest-element-in-an-array/description/?envType=study-plan-v2&envId=top-100-liked)

## 题目大意
Given an integer array `nums` and an integer `k`, return the `kth` largest element in the array.

Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Can you solve it without sorting?

Example 1:
```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
```
Example 2:
```
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```

## 解题思路
1.quick sort(超时)

2.quick select(quick sort improvement)

3.heap

## 代码
### 思路1: 快速排序
```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        return sorted(nums)[len(nums)-k]
```
* Time Complexity: $O(n \log n)$, where $n$ is the number of elements in the list `nums`
* Space Complexity: $O(\log n)$, where $n$ is the number of elements in the list `nums`

### 思路2: 快速选择
```python
class Solution:
    def findKthLargest(self, nums, k):
        def quick_select(nums, k):
            pivot = random.choice(nums)     # 随机选择基准数
            big, equal, small = [], [], []  # 将大于、小于、等于 pivot 的元素划分至 big, small, equal 中
            for num in nums:
                if num > pivot:
                    big.append(num)
                elif num < pivot:
                    small.append(num)
                else:
                    equal.append(num)
            if k <= len(big):               # 第 k 大元素在 big 中，递归划分
                return quick_select(big, k)
            if len(nums) - len(small) < k:  # 第 k 大元素在 small 中，递归划分
                return quick_select(small, k - len(nums) + len(small))
            return pivot                    # 第 k 大元素在 equal 中，直接返回 pivot
        return quick_select(nums, k)


if __name__ == "__main__":
    import random
    nums = [2, 4, 1, 0, 3, 5]
    k = 3

    solution = Solution()
    num = solution.findKthLargest(nums, k)
    print(f"The kth largest number is {num}")
```
* Time Complexity: $O(n)$, where $n$ is the number of elements in the list `nums`
* Space Complexity: $O(n)$, where $n$ is the number of elements in the list `nums`

### 思路3: 堆