---
title: 48 找到字符串中所有字母异位词
source: https://leetcode.cn/problems/find-all-anagrams-in-a-string/description/?envType=study-plan-v2&envId=top-100-liked
algorithm:
  - "[[sliding-window]]"
tags:
  - algorithm-exercise/sliding-window
difficulty: medium
star: true
---

## Solution

```cpp
class Solution
{
public:
    vector<int> findAnagrams(string s, string p)
    {
        vector<int> ans;

        // How many current character's sum in the window
        // is different with target
        int unmatching_character_count = 0;

        // Build target character dictionary
        int tar_dic[26]; memset(tar_dic, 0, sizeof(tar_dic));
        for (int i = 0; i < p.length(); i++)
        {
            tar_dic[p[i]-'a'] += 1;
            unmatching_character_count += 1;
        }

        // Slide the window and find the answer
        int cur_dic[26]; memset(cur_dic, 0, sizeof(cur_dic));
        int l = 0, r = 0;
        while (r < s.length())
        {
            cur_dic[s[r]-'a'] += 1;
            if (cur_dic[s[r]-'a'] == tar_dic[s[r]-'a'])
                unmatching_character_count -= tar_dic[s[r]-'a'];
            r += 1;

            if (r-l == p.length())
            {
                if (unmatching_character_count == 0)
                    ans.emplace_back(l);

                // Move the left boundary
                // since window width will exceed the limit
                cur_dic[s[l]-'a'] -= 1;
                if (cur_dic[s[l]-'a'] + 1 == tar_dic[s[l]-'a'])
                    unmatching_character_count += tar_dic[s[l]-'a'];
                l += 1;
            }
        }

        return ans;
    }
};
```
