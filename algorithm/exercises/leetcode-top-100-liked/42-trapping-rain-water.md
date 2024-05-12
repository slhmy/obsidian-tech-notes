---
title: 42 接雨水
source: https://leetcode.cn/problems/trapping-rain-water/?envType=study-plan-v2&envId=top-100-liked
algorithm:
  - "[[two-pointers]]"
  - "[[monotonic-stack]]"
tags:
  - algorithm-exercise/two-pointers
  - algorithm-exercise/monotonic-stack
difficulty: hard
star: true
---

## Solution

```cpp
class Solution
{
public:
    int trap(vector<int>& height)
    {
        int ans = 0;
        stack<int> top_lower_idx_stack;
        for (int i = 0; i < height.size(); i++)
        {
            int cur_height = 0;
            // Pop all blocks in the left
            // which is lower than current block
            while (!top_lower_idx_stack.empty())
            {
                int left_idx = top_lower_idx_stack.top();
                if (height[left_idx] < height[i])
                {
                    ans += (height[left_idx] - cur_height) * (i - left_idx - 1);
                    cur_height = height[left_idx];
                    top_lower_idx_stack.pop();
                }
                else
                {
                    // If left side block is higher, break the loop
                    ans += (height[i] - cur_height) * (i - left_idx - 1);
                    break;
                }
            }
            top_lower_idx_stack.emplace(i);
        }
        return ans;
    }
};
```
