---
title: 283 移动零
source: https://leetcode.cn/problems/move-zeroes/?envType=study-plan-v2&envId=top-100-liked
algorithm:
  - "[[two-pointers]]"
tags:
  - algorithm-exercise/two-pointers
difficulty: easy
star: false
---

## Solution

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        n = len(nums)

        # Swapping zero with its
        # nearest none-zero number in following numbers
        p = 0; q = 1
        while p < n and q < n:
            if not nums[p] == 0:
                p += 1; continue

            if q < p + 1:
                q = p + 1
            while q < n:
                if nums[q] == 0:
                    q += 1; continue
                nums[p], nums[q] = nums[q], nums[p]
                break

            p += 1
```
