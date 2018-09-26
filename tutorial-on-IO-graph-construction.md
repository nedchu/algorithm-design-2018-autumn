# 教程：输入输出及图构建
## 常见的两种输入方式
循环读入中，需要读入多组数据直到文件尾，新手有时不会循环读入会吃亏。

C 语言中可以这么写：
```cpp
#include <stdio.h>
int main() {
    int a, b;
    while (scanf("%d%d", &a, &b) != EOF)
        printf("%d\n", a + b);
    return 0;
}
```

C++ 语言中可以这么写：
```cpp
#include <iostream>
using namespace std;
int main() {
    int a, b;
    while (cin >> a >> b)
        cout << a + b << endl;
    return 0;
}
```


第二种方式是先读入一个组数再进行输入，这种方式对于不了解的新手比较友好，C 语言具体写法如下：
```cpp
#include <stdio.h>

int main() {
  int t, a, b;
  scanf("%d", &t);
  while (t--) {
    scanf("%d%d", &a, &b);
    printf("%d\n", a + b);
  }
  return 0;
}
```
C++ 语言可以这么写：
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
  int t, a, b;
  cin >> t;
  while (t--) {
    cin >> a >> b;
    cout << (a + b) << endl;
  }
  return 0;
}
```

## 关于输入输出及语言的讨论
当输入输出数据较大的时候建议使用C语言的 `scanf,printf` 函数。

C++ 语言中有许多比较方便的 STL 函数并且能够兼容 C 语言，建议大家直接写 C++ 即可。

## 图构建
图构建的第一种方式是邻接矩阵，这种方式使用一个二维数组即可，此处不多介绍了。

图构建的第二种方式是邻接表，课本上会说拉一个链表出来，直接实现相对比较麻烦，一种比较好的方式是使用标准库中的动态数组 `vector`。

加入头文件：
```cpp
#include <vector>
```
以下为声明，其中 `N` 就是点数的上限，`graph[i]` 中保存了 i 号节点能够到达哪些节点：
```cpp
const int N = 1e3+5;

vector<int> graph[N];
```

构建图，对于有向边 `<u,v>` 可以如下加入一条边：
```cpp
graph[u].push_back(v);
```
如果是一条无向边 `(u,v)` 可以如下加入一条边：
```cpp
graph[u].push_back(v);
graph[v].push_back(u);
```
遍历邻居的时候可以这么写，其中下面一种写法需要C++11支持：
```cpp
for (int i = 0; i < graph[u].size(); i++) {
    int nbr = graph[u][i];
}
for (auto &nbr: graph[u]) {

}
```
初始化邻接表的时候可以：
```cpp
for (int i = 0; i < N; i++) {
    graph[i].clear();
}
```
基本的操作如上，足够处理大部分题目，如有进一步需求可以查阅文档进行学习。

另外有一种实现方式叫做链式前向星，是一种实现很好的邻接表，空间时间上比使用 `vector` 有一定优势，但是难写一点，有兴趣的同学可以自行了解。