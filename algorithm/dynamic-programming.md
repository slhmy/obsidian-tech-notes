---
title: Dynamic Programming
tags:
  - algorithm
---

## Shortest Edit Distance

$dp[i,j] = min(dp[i,j-1]+1,dp[i-1,j]+1,dp[i-1,j-1]+s[i]==t[j])$

> i, j indicating the letter index.
> If we start from 0, we will encounter overflow issue.
> **So, we need to index the word from 1.**
> **(which means when looking at index i, we are actually visiting s[i-1])**

### Memory Optimize

Or many people says, is the **Scrolling Array**.
Dimensions can be reduced
since most of the time we only consider limited previous states in DP.

For example in [[72-edit-distance]],
states from the previous dimension can be flushed
by the calculating one in current dimension.
States are replaced round and round with the switch of each dimension,
so it was like data in the array scrolling in the calculation.

Scrolling array may not be so easy in many circumstance.
**You need to pre-record some of the data you need to reference**
**since they may be flushed too quickly.**
