---
title: 560 和为 K 的子数组
source: https://leetcode.cn/problems/subarray-sum-equals-k/description/?envType=study-plan-v2&envId=top-100-liked
algorithm:
  - "[[prefix-sum]]"
  - "[[hash-map]]"
tags:
  - algorithm-exercise/prefix-sum
  - algorithm-exercise/hash-map
difficulty: medium
star: false
---

`nums[i]` can be negative so [[sliding-window]] will not work here
(because it's hard to tell when to move the boundary).

[[prefix-sum]] is another way to quickly locate the boundary.
If work with [[hash-map]] while spending more memory,
finding the boundary can be speed up to $O(n)$.

## Solution

```cpp
class Solution
{
public:
    int subarraySum(vector<int>& nums, int k)
    {
        unordered_map<int, int> prefixSumCount;
        int sum = 0, ans = 0;

        prefixSumCount[0] = 1;
        for (int i = 0; i < nums.size(); i++)
        {
            sum += nums[i];
            if (prefixSumCount.count(sum-k))
                ans += prefixSumCount[sum-k];
            prefixSumCount[sum] += 1;
        }

        return ans;
    }
};
```
