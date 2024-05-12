---
title: 1 两数之和
source: https://leetcode.cn/problems/two-sum/description/?envType=study-plan-v2&envId=top-100-liked
algorithm:
  - "[[hash-map]]"
tags:
  - algorithm-exercise/hash-map
difficulty: easy
star: false
---

## Solution

```cpp
class Solution
{
public:
    vector<int> twoSum(vector<int>& nums, int target)
    {
        unordered_map<int, int> val_idx_map;

        for (int i = 0; i < nums.size(); ++i)
        {
            auto it = val_idx_map.find(target - nums[i]);
            if (it != val_idx_map.end()) return { it->second, i };
            val_idx_map[nums[i]] = i;
        }

        return {};
    }
};
```
