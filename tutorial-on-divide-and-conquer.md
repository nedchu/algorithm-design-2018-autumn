# 分治

分治是指一类利用了分而治之思想的算法，将问题切分为若干个不相交的子问题解决，并且将结果合并后获得最终的结果。

常见的分治算法有快排，归并，二分等等，此处为方便大家，介绍一些常用的STL函数

## 朴素二分

函数如果满足单调性可以利用二分搜索进行剪枝。

二分的关键在于寻找一个合适的角度，令问题符合单调性的性质。二分实现时的边界问题会令初学者比较头疼。

第一点是算法设计的问题，此处不展开。关于第二点，我常用的方法是记录一个结果值，满足条件就更新它。

比如如果要找满足条件的最大的值，可以如下进行：

```cpp
int l = 0, r = 1e5, ans;
while (l <= r) {
    int mid = (l + r) / 2;
    if (check(mid) <= bound) {
        l = mid + 1;
        ans = mid;
    } else {
        r = mid - 1;
    }
}
```

关于浮点数的二分，有一个问题就是浮点数很难完全相等，一种方式是在上下界的距离达到某个界限后停止，停止条件为`r - l < eps`，一般取`eps=1e-10~1e-6`之类的。

实际只要精度足够就可以停止，还有一种方式是直接限定迭代次数，由于$2^{100}\approx 10^30$，已经是一个很高的精度，通常直接迭代100次即可，如果题目时间或者精度有比较特别的要求，只需要调整迭代次数即可。

相比调整精度而言，调整迭代次数更加简单直接和可预期。

## 二分库函数

二分的算法需要包含库 `#include <algorithm>`。调用二分算法之前需要先使用 `sort` 进行排序。

最基础的二分查找可以调用，返回是否找到：

```cpp
sort(a, a + n);
if (binary_search(a, a + n, target)) {
    found;
} else {
    not found;
}
```

另外有两个函数分别查找$\geq x$以及$> x$的第一个位置的迭代器，将它减去头指针能够获得位置：
```cpp
sort(a, a + n); // 1 3 5 7
lower_bound(a, a + n, 3); // return &a[1];
int p = lower_bound(a, a + n, 2) - a; // p = 1;
upper_bound(a, a + n, 3); // return &a[2];
int w = upper_bound(a, a + n, 2) - a; // w = 1;
```

## 归并排序

归并排序是十分基础的分治算法，利用标准库可以比较方便地实现：
```cpp
merge(sorted_list_1, sorted_list_1 + n, sorted_list_2, sorted_list_2 + m, output);
copy(array, array + k, output);
```
一个归并排序算法的实现如下：
```cpp
// sort a[l] ... a[r-1]
void merge_sort(int *a, int l, int r)
{
  if (r - l <= 1) return;
  int mid = (l + r) / 2;
  merge_sort(a, l, mid);
  merge_sort(a, mid, r);
  merge(a + l, a + mid, a + mid, a + r, b + l);
  copy(b + l, b + r, a + l);
}
```
