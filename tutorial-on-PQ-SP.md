# 优先队列，最短路

## 优先队列

优先队列就是大根堆，支持在对数时间内取出最大值，插入元素。

使用 `#include <queue>` 后就能够使用优先队列了：

```cpp
priority_queue<int> pq; // 声明一个保存int的优先队列
pq.push(1);
pq.push(2);
pq.push(2); // add 1, 2, 2
int t = pq.top(); // 获得最优先（大）元素 t = 2
pq.pop(); // 2 is poped
pq.pop(); // 2 is poped
int s = pq.size(); // 获得优先队列大小 s = 1
pq.pop(); // 1 is poped
```

优先队列可以用于内置类型和定义了顺序的结构体，优先队列的模板中实际包含三个参数，分别是元素类型，容器类型和比较算子。

通过更改比较算子能够改变对优先级的定义，优先队列操作都是一致的，小根堆声明方式如下：

```cpp
priority_queue<int, vector<int>, greater<int>> q; // 小根堆
```

给第三个参数传入类似 [排序](tutorial-topo-SCC.md) 中的比较算子就能定义自己的优先级了。

