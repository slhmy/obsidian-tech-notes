---
title: Useful Grammar for C++
tags:
  - grammar/cpp
---

### Customize `Compare` for `priority_queue`

Source: [347. 前 K 个高频元素 - 力扣（LeetCode）](https://leetcode.cn/problems/top-k-frequent-elements/?envType=study-plan-v2&envId=top-100-liked)

```cpp
static bool cmp(pair<int, int> &m, pair<int, int> &n)
{
    return m.second > n.second;
}

vector<int> topKFrequent(vector<int> &nums, int k)
{
    // ...
    priority_queue<pair<int, int>,
                   vector<pair<int, int>>,
                   decltype(&cmp)> // bool (*)(pair<int, int> &, pair<int, int> &)
        q(cmp);
    // ...
}
```

### Auto Traverse over `map`

Source: [347. 前 K 个高频元素 - 力扣（LeetCode）](https://leetcode.cn/problems/top-k-frequent-elements/?envType=study-plan-v2&envId=top-100-liked)

```cpp
unordered_map<int, int> occurrences;

for (auto &[num, count] : occurrences)
{
    // ...
}
```
