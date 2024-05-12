---
title: 分布式缓存
tags:
  - caching
---

[一致性哈希算法（consistent hashing） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/129049724)

## 简单的哈希函数

`m = hash(o) % n`

集群节点变更会造成大量的数据迁移

## 一致性哈希

哈希 Key 到一个 $2^{32}$ 个桶的空间中，首位相连，形成一个环。
这样在节点伸缩时只会影响相邻节点。

桶中数据按一个固定的方向去寻找存储的节点（通常是顺时针）。
缺点是当节点分布不均匀时
（比如原来有五个节点，3，4号节点全部不可用了），
会出现数据倾斜。

## 虚拟节点

通过哈希算法，为每个物理节点在一致性哈希中提到的环上，
生成较多数目的虚拟节点，使节点保持在一个相对均匀的分布状况。
这样在重新分配数据时，有较为均匀的概率影响到其他节点。

参考仓库：
[serialx/hashring (github.com)](https://github.com/serialx/hashring)