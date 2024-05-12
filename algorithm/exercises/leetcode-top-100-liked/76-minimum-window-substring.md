---
title: 76 最小覆盖子串
source: https://leetcode.cn/problems/minimum-window-substring/?envType=study-plan-v2&envId=top-100-liked
algorithm:
  - "[[sliding-window]]"
tags:
  - algorithm-exercise/sliding-window
difficulty: hard
star: false
---

A transform of [[48-find-all-anagrams-in-a-string]].
Slightly different on when to deal with the mighty answer.

## Solution

```cpp
class Solution
{
public:
    string minWindow(string s, string p)
    {
        // Mark wether we got an answer
        int ans_l = -1, ans_r = 0;

        // How many current character's sum in the window
        // is different with target
        int unmatching_character_count = 0;

        // Build target character dictionary
        // A-Z..a-z contains 58 characters
        int tar_dic[58]; memset(tar_dic, 0, sizeof(tar_dic));
        for (int i = 0; i < p.length(); i++)
        {
            tar_dic[p[i]-'A'] += 1;
            unmatching_character_count += 1;
        }

        // Slide the window and find the answer
        int cur_dic[58]; memset(cur_dic, 0, sizeof(cur_dic));
        int l = 0, r = 0;
        while (r < s.length())
        {
            cur_dic[s[r]-'A'] += 1;
            if (cur_dic[s[r]-'A'] == tar_dic[s[r]-'A'])
                unmatching_character_count -= tar_dic[s[r]-'A'];

            while (unmatching_character_count == 0) {
                // Update the answer if the newer one is better
                if (r-l+1 < ans_r-ans_l+1 || ans_l == -1)
                    ans_r = r, ans_l = l;

                cur_dic[s[l]-'A'] -= 1;
                if (cur_dic[s[l]-'A'] + 1 == tar_dic[s[l]-'A'])
                    unmatching_character_count += tar_dic[s[l]-'A'];
                l += 1;
            }

            r += 1;
        }

        if (ans_l != -1)
            return s.substr(ans_l, ans_r-ans_l+1);
        return "";
    }
};
```
