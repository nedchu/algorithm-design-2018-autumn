# BFS
# 队列
C++中队列的头文件为`#include <queue>`，其中包含了队列以及优先队列（堆）。

```cpp
queue<int> q;// declare
q.push(1);// insert item, q: 1
q.push(2);// q: 1 2
int f = q.front();// get fron of queue, f == 1
q.pop();// 1 is poped from queue, q: 2
int n = q.size();// get size, n == 1
q.pop();// 2 is poped from quere, q is empty now
q.empty();// check empty, returns true;
```

# BFS求最短路
当图中的边不带权重的时候，可以使用bfs进行单源最短路的求解。一个数组进行标记，将点加入队列的时候就能同时获得最短路。

```cpp
vis[] 是否访问
dis[] 最短路
g[] 邻接表
INF = 0x3f3f3f3f

fill vis with false
fill dis with INF

queue<int> q;
push s into q, update vis[s], dis[s]
while (!q.empty()) {
    cur := front of q, then pop it
    for (every neightbour nbr of cur) {
        if nbr is not visited
            push nbr into q, update vis[nbr], dis[nbr]
    }
}
```

## 棋盘类问题
棋盘类问题中通常会需要访问周围四个位置，需要分别考虑：
```cpp
(x, y+1), (x, y-1), (x+1, y), (x-1, y)
check next point and update
```
如果写死代码一个个枚举需要大量复制粘贴，如果有条件限制就更加麻烦难写。

一种常见的技巧是使用一个方向数组：

```cpp
int D = 4;
int dx[D] = {0, 0, 1, -1};
int dy[D] = {1, -1, 0, 0};
```

在进行搜索的时候可以如下进行：
```cpp
currently at (x, y)
for (dir := 0, 1, 2, 3)
    next_pos = (x + dx[dir], y + dy[dir])
    if next_pos is valid place:
        push it into queue and update
```

通过方向数组能够将显式枚举的过程转变为循环，所有判断更新的代码只需要书写一遍，能够减少错误的发生。

除此之外常见的还有八连通和跳马，所有的移动信息都可以压缩进方向数组进行方便的实现。