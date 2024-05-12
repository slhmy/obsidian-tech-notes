---
title: 3 无重复字符的最长子串
source: https://leetcode.cn/problems/longest-substring-without-repeating-characters/?envType=study-plan-v2&envId=top-100-liked
algorithm:
  - "[[sliding-window]]"
tags:
  - algorithm-exercise/sliding-window
difficulty: medium
star: false
---

## Solution

```cpp
class Solution
{
public:
    int lengthOfLongestSubstring(string s)
    {
        unordered_set<char> exist;
        int p = 0, ans = 0;
        for (int i = 0; i < s.length(); i++)
        {
            // Move left boundary
            // util duplicate character is deleted
            if (exist.count(s[i])) {
                while(exist.count(s[i])) exist.erase(s[p++]);
            }
            exist.emplace(s[i]);
            ans = max(ans, i-p+1);
        }
        return ans;
    }
};
```
