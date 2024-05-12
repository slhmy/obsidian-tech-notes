---
title: Vector & Array in C++
tags:
  - grammar/cpp
---

> [!caution]
> 在 C++ 中，你应该尽量使用 `std::vector` 和 `std::array`，而不是 C 风格的数组。原因是 C 风格的数组没有提供任何安全保障，没有越界检查，尽管在算法题中我们经常会用下标访问数组元素（`std::vector` 和 `std::array` 中正规的做法是使用 `at(idx)` 方法）。

## vector 和 array 的区别

`std::vector` 存储在堆上，`std::array` 存储在栈上。
因此，当你需要一个动态大小的数组时，你应该使用 `std::vector`，而当你只需要一个固定大小的数组时，使用 `std::array` 会更好，它拥有更好的性能。

## vector 和 array 的初始化

```cpp
// 初始化一个大小为 10 的 vector，所有元素的值都是 0
std::vector<int> v1(10);
// 初始化一个大小为 10 的 vector，所有元素的值都是 1
std::vector<int> v2(10, 1);
// 初始化一个大小为 10 的 array，所有元素的值都是 0
std::array<int, 10> a1;
// 通过一个已有的 array 初始化另一个 array
std::array<int, 10> a3 = a2;
// 通过一个已有的 vector 初始化另一个 vector
std::vector<int> v3 = v2;
```

同时 `std::array` 还支持通过 `fill(n)` 方法填充数组。

## vector 的插入和删除

```cpp
// 在末尾插入一个元素
v.push_back(1); v.emplace_back(1);
// 在末尾删除一个元素
v.pop_back();
// 在指定位置插入一个元素
v.insert(v.begin() + 1, 2);
// 在指定位置删除一个元素
v.erase(v.begin() + 1);
// 在指定位置插入另一组vector
v.insert(v.begin() + 1, v2.begin(), v2.end());
auto rg = std::list{1, 2, 3};
v.insert_range(v.begin() + 1, rg);
```
