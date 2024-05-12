---
title: 72 编辑距离
source: https://leetcode.cn/problems/edit-distance/description/?envType=study-plan-v2&envId=top-100-liked
algorithm:
  - "[[dynamic-programming]]"
tags:
  - algorithm-exercise/dynamic-programming
difficulty: medium
star: true
---

## Solution

### Without memory optimize

```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int n = word1.length(), m = word2.length();
        int dp[n+1][m+1];
        for (int i = 0; i <= n; i++) dp[i][0] = i;
        for (int j = 0; j <= m; j++) dp[0][j] = j;

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (word1[i-1] == word2[j-1])
                    dp[i][j] = dp[i - 1][j - 1];
                else
                    dp[i][j] = min(
                        min(dp[i][j - 1], dp[i - 1][j]),
                        dp[i - 1][j - 1]
                    ) + 1;
            }
        }

        return dp[n][m];
    }
};
```

### With memory optimize

```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int n = word1.length(), m = word2.length();
        int dp[m+1];
        for (int j = 0; j <= m; j++) dp[j] = j;

        for (int i = 1; i <= n; i++) {
            // We cannot store both `dp[i-1][j-1]` & `dp[i][j-1]`
            // at the same time, in a single dimension array.
            // So we store `dp[i-1][j-1]` in another variable
            // since `dp[i][j-1]` is flushed every time
            // when the ealier `dp[j]` calculate is finished.
            int left_up = dp[0];
            dp[0] = i;
            for (int j = 1; j <= m; j++) {
                // Remember next `dp[i-1][j-1]`
                // in the start of this round
                int next_left_up = dp[j];
                if (word1[i-1] == word2[j-1])
                    dp[j] = left_up;
                else
                    dp[j] = min(
                        min(dp[j - 1], dp[j]),
                        left_up
                    ) + 1;
                // `dp[i-1][j-1]` is flushed by `dp[i][j-1]`.
                // So we need to set it from another memory variable.
                left_up = next_left_up;
            }
        }

        return dp[m];
    }
};
```
