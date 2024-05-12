---
title: 128 最长连续序列
source: https://leetcode.cn/problems/longest-consecutive-sequence/?envType=study-plan-v2&envId=top-100-liked
algorithm:
  - "[[hash-map]]"
tags:
  - algorithm-exercise/hash-map
difficulty: medium
star: false
---

## Solution

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        existSet = set(nums)
        ans = 0
        for num in nums:
            # Make sure `num` is the head of the sequence
            if num-1 not in existSet:
                count = 1; p = num
                while p+1 in existSet:
                    count += 1; p += 1
                ans = max(count, ans)

        return ans
```
