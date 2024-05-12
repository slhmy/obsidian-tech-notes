---
title: 11 盛最多水的容器
source: https://leetcode.cn/problems/container-with-most-water/description/?envType=study-plan-v2&envId=top-100-liked
algorithm:
  - "[[two-pointers]]"
  - "[[greedy]]"
tags:
  - algorithm-exercise/two-pointers
  - algorithm-exercise/greedy
difficulty: medium
star: false
---

## Solution

```rust
impl Solution {
    pub fn max_area(height: Vec<i32>) -> i32 {
        let mut res = 0;
        let mut r = 0;
        let mut l = height.len() - 1;
        while r < l {
            // Calculate the volume and replace res if it's larger
            res = res.max(height[r].min(height[l]) * (l - r) as i32);
            // When squeezing the boundary, leave the higher one
            // This is because we will not get a larger volume
            // if we leave the lower one
            if height[r] < height[l] {
                r += 1;
            } else {
                l -= 1;
            }
        }
        res
    }
}
```
