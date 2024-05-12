---
title: 49 字母异位词分组
source: https://leetcode.cn/problems/group-anagrams/description/?envType=study-plan-v2&envId=top-100-liked
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
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        d = {}
        for s in strs:
            key = tuple(sorted(s))
            d[key] = d.get(key, []) + [s]
        return list(d.values())
```
