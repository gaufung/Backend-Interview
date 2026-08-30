1. [如何只用栈实现队列？再只用队列实现栈？](#1-如何只用栈实现队列再只用队列实现栈)
2. [请写一段会导致栈溢出的代码。](#2-请写一段会导致栈溢出的代码)
3. [请写一个尾递归版本的阶乘（Factorial）函数。](#3-请写一个尾递归版本的阶乘factorial函数)
4. [请用你熟悉的语言实现一个简单的 REPL，并支持 RPN 表达式求值。](#4-请用你熟悉的语言实现一个简单的-repl并支持-rpn-表达式求值)
5. [如何设计一个磁盘碎片整理工具？](#5-如何设计一个磁盘碎片整理工具)
6. [如何编写一个随机生成迷宫的程序？](#6-如何编写一个随机生成迷宫的程序)
7. [请写一个会导致内存泄漏的例子。](#7-请写一个会导致内存泄漏的例子)
8. [如何生成一系列不同的随机数？](#8-如何生成一系列不同的随机数)
9. [如何实现一个非常简单的垃圾回收器？](#9-如何实现一个非常简单的垃圾回收器)
10. [如何实现一个基础的消息 Broker？](#10-如何实现一个基础的消息-broker)
11. [如何实现一个基础的 Web 服务器，并规划后续功能？](#11-如何实现一个基础的-web-服务器并规划后续功能)
12. [如何对 10GB 文件排序？如果是 10TB 呢？](#12-如何对-10gb-文件排序如果是-10tb-呢)
13. [如何自动检测重复文件？](#13-如何自动检测重复文件)

---

## 1 如何只用栈实现队列？再只用队列实现栈？

这类题的重点不只是写代码，而是理解：

- 栈：LIFO
- 队列：FIFO
- 如何通过中间缓冲改变访问顺序

### 用两个栈实现队列

核心思路：

- `in` 栈负责入队
- `out` 栈负责出队
- 当 `out` 为空时，把 `in` 全部倒进去

```go
package main

import "errors"

type Stack []int

func (s *Stack) Push(v int) {
    *s = append(*s, v)
}

func (s *Stack) Pop() (int, error) {
    if len(*s) == 0 {
        return 0, errors.New("empty")
    }
    n := len(*s) - 1
    v := (*s)[n]
    *s = (*s)[:n]
    return v, nil
}

type Queue struct {
    in  Stack
    out Stack
}

func (q *Queue) Enqueue(v int) {
    q.in.Push(v)
}

func (q *Queue) Dequeue() (int, error) {
    if len(q.out) == 0 {
        for len(q.in) > 0 {
            v, _ := q.in.Pop()
            q.out.Push(v)
        }
    }
    return q.out.Pop()
}
```

摊还复杂度：

- `Enqueue`：O(1)
- `Dequeue`：均摊 O(1)

### 用两个队列实现栈

核心思路：

- 入栈时把新元素放进空队列
- 再把旧队列里的元素全部搬过去
- 始终保证队头就是“栈顶”

```go
package main

import "errors"

type Queue2 []int

func (q *Queue2) Enqueue(v int) {
    *q = append(*q, v)
}

func (q *Queue2) Dequeue() (int, error) {
    if len(*q) == 0 {
        return 0, errors.New("empty")
    }
    v := (*q)[0]
    *q = (*q)[1:]
    return v, nil
}

type StackByQueue struct {
    q1 Queue2
    q2 Queue2
}

func (s *StackByQueue) Push(v int) {
    s.q2.Enqueue(v)
    for len(s.q1) > 0 {
        x, _ := s.q1.Dequeue()
        s.q2.Enqueue(x)
    }
    s.q1, s.q2 = s.q2, s.q1
}

func (s *StackByQueue) Pop() (int, error) {
    return s.q1.Dequeue()
}
```

### 面试回答要点

> 这道题考查的是数据结构行为转换。用两个栈实现队列的关键是“延迟搬运”，用两个队列实现栈的关键是“重排队列顺序”。

---

## 2 请写一段会导致栈溢出的代码。

最简单的方式是无终止条件递归：

```go
package main

func boom() {
    boom()
}

func main() {
    boom()
}
```

### 为什么会栈溢出

每次函数调用都要消耗栈空间来保存：

- 返回地址
- 局部变量
- 调用上下文

如果递归没有终止条件，调用栈会无限增长，最终触发 stack overflow。

### 现代补充

- 即使有递归终止条件，递归深度过大也可能溢出
- 某些语言会做尾调用优化，但不是所有语言都会
- 生产代码里应关注递归深度和数据规模

### 面试回答要点

> 栈溢出最经典的触发方式就是无界递归，因为每次调用都会消耗新的栈帧，直到超过运行时或操作系统的栈限制。

---

## 3 请写一个尾递归版本的阶乘（Factorial）函数。

先给普通递归版本：

```go
func Factorial(n int) int {
    if n <= 1 {
        return 1
    }
    return n * Factorial(n-1)
}
```

这不是尾递归，因为递归调用返回后还要再乘 `n`。

### 尾递归版本

```go
func FactorialTail(n int) int {
    return factorialAcc(n, 1)
}

func factorialAcc(n int, acc int) int {
    if n <= 1 {
        return acc
    }
    return factorialAcc(n-1, acc*n)
}
```

### 为什么这是尾递归

因为递归调用是函数中的最后一步，没有后续计算。

### 但工程上要注意

Go 不保证尾调用优化，所以在超深递归场景下，显式循环通常更稳妥：

```go
func FactorialIter(n int) int {
    result := 1
    for i := 2; i <= n; i++ {
        result *= i
    }
    return result
}
```

### 面试回答要点

> 尾递归通过累加器把中间状态前移，使递归调用成为最后一步；但是否真正节省栈空间，还取决于语言和编译器是否支持尾调用优化。

---

## 4 请用你熟悉的语言实现一个简单的 REPL，并支持 RPN 表达式求值。

RPN（Reverse Polish Notation，逆波兰表达式）的特点是操作符写在操作数后面，例如：

```text
3 4 +
```

### 一个简单 Python 版本

```python
def eval_rpn(expr: str) -> float:
    stack = []
    for token in expr.split():
        if token in {"+", "-", "*", "/"}:
            if len(stack) < 2:
                raise ValueError("invalid expression")
            b = stack.pop()
            a = stack.pop()
            if token == "+":
                stack.append(a + b)
            elif token == "-":
                stack.append(a - b)
            elif token == "*":
                stack.append(a * b)
            else:
                stack.append(a / b)
        else:
            stack.append(float(token))

    if len(stack) != 1:
        raise ValueError("invalid expression")
    return stack[0]


def repl():
    print("RPN REPL, input 'quit' to exit")
    while True:
        line = input("> ").strip()
        if line in {"quit", "exit"}:
            break
        try:
            print(eval_rpn(line))
        except Exception as e:
            print(f"error: {e}")


if __name__ == "__main__":
    repl()
```

### 可以继续扩展什么

- 支持整数和浮点数区分
- 支持变量
- 支持更多操作符
- 支持历史记录
- 支持多行输入和帮助命令

### 面试回答要点

> 这类题的核心是用栈求值。REPL 负责读取、执行、打印、循环；RPN 负责把表达式转成一系列栈操作。

---

## 5 如何设计一个磁盘碎片整理工具？

这题重点不在“写个脚本移动文件”，而在于你是否理解：

- 文件系统元数据
- 磁盘块布局
- 崩溃恢复
- 数据安全

### 设计目标

碎片整理工具的目标通常是：

- 减少文件碎片
- 提高顺序读写性能
- 更有效利用连续空间

但在现代 SSD 上，这个目标就不一定仍然成立。

### 第一步：先看文件系统和硬件类型

必须先明确：

- 是 NTFS、EXT4、XFS 还是别的文件系统
- 是 HDD 还是 SSD

#### 为什么这很重要

- HDD 随机寻道代价高，碎片更影响性能
- SSD 没有机械寻道，碎片影响通常小得多
- SSD 频繁搬移数据反而可能增加写放大和寿命损耗

### 工具核心流程

#### 1. 扫描文件系统元数据

识别：

- 文件占用了哪些块
- 哪些文件被分散存储
- 哪些区域有连续空闲空间

#### 2. 生成搬迁计划

目标是减少搬迁次数、减少风险，并尽量把热点文件放到连续区域。

#### 3. 事务化或日志化移动

在移动块数据时，必须考虑：

- 宕机恢复
- 中断恢复
- 元数据一致性

### 关键难点

- 文件在整理过程中可能仍被读写
- 元数据更新必须原子化或可恢复
- 整理过程本身会产生 I/O 压力
- 需要避免把磁盘“整理死”

### 面试回答要点

> 设计磁盘碎片整理工具，关键不只是搬文件，而是理解文件系统元数据、崩溃恢复和硬件差异。尤其在现代 SSD 场景下，是否需要整理本身就是设计问题的一部分。

---

## 6 如何编写一个随机生成迷宫的程序？

随机迷宫生成的核心目标通常是：

- 生成连通路径
- 保证结构随机性
- 控制是否存在唯一解或多解

### 常见算法

- DFS 回溯法
- Prim 算法
- Kruskal 算法
- Recursive Division

### 一个简单思路：DFS 回溯

1. 从一个起点开始
2. 随机选择一个未访问邻居
3. 打通两者之间的墙
4. 继续深入
5. 如果没有未访问邻居，就回溯

### 一个简单 Python 示例

```python
import random


def generate_maze(width, height):
    maze = [[1 for _ in range(width)] for _ in range(height)]
    visited = [[False for _ in range(width)] for _ in range(height)]

    dirs = [(0, 2), (0, -2), (2, 0), (-2, 0)]

    def dfs(x, y):
        visited[y][x] = True
        maze[y][x] = 0

        order = dirs[:]
        random.shuffle(order)
        for dx, dy in order:
            nx, ny = x + dx, y + dy
            if 0 < nx < width and 0 < ny < height and not visited[ny][nx]:
                maze[y + dy // 2][x + dx // 2] = 0
                dfs(nx, ny)

    dfs(1, 1)
    return maze
```

其中：

- `1` 表示墙
- `0` 表示通路

### 面试回答要点

> 迷宫生成本质上是图遍历问题。常见做法是把格子看成图节点，再通过 DFS、Prim 或 Kruskal 随机生成一棵生成树，从而形成迷宫路径。

---

## 7 请写一个会导致内存泄漏的例子。

### C/C++ 中最直接的泄漏

```cpp
#include <string>
using namespace std;

class MyClass {
public:
    int num;
    string text;
};

void leak() {
    MyClass* p = new MyClass();
    // do something
    // 忘记 delete
}
```

这里 `new` 分配的对象没有释放，会造成泄漏。

### 托管语言里也可能泄漏

GC 语言并不意味着绝对不会泄漏，常见原因包括：

- 长生命周期对象持有短生命周期对象引用
- 缓存无限增长
- 事件监听器未取消
- 文件句柄 / socket / DB 连接未释放

例如 Java / C# 中的“逻辑泄漏”：

```java
import java.util.*;

public class LeakExample {
    private static final List<byte[]> cache = new ArrayList<>();

    public static void main(String[] args) {
        while (true) {
            cache.add(new byte[1024 * 1024]);
        }
    }
}
```

这不是“忘记 free”，但因为对象一直可达，也会导致内存持续增长。

### 面试回答要点

> 内存泄漏的本质不是“内存没被 free”这么简单，而是“本该释放的资源长期无法回收”。在手动内存管理语言里常见于忘记释放，在 GC 语言里常见于意外持有引用或资源未关闭。

---

## 8 如何生成一系列不同的随机数？

这题要先区分两个概念：

- **伪随机数（PRNG）**
- **密码学安全随机数（CSPRNG）**

大多数算法题讨论的是 PRNG。

### 常见伪随机方法

#### 1. 线性同余生成器（LCG）

公式：

```text
X_{n+1} = (aX_n + c) mod m
```

示例：

```go
func Next(seed uint64) uint64 {
    const a = 1664525
    const c = 1013904223
    const m = 1 << 32
    return (a*seed + c) % m
}
```

#### 2. Xorshift

```go
func XorShift32(x uint32) uint32 {
    x ^= x << 13
    x ^= x >> 17
    x ^= x << 5
    return x
}
```

### 如果要求“不同的随机数”

如果题目意思是“生成不重复随机数”，做法通常是：

- 先生成序列再 shuffle
- 或者用集合去重
- 或者在范围内做 Fisher-Yates 洗牌

例如从 `0..n-1` 生成一组不重复乱序数，最经典的是洗牌算法。

### 现代工程提醒

- 不要自己造密码学随机数
- token、密钥、验证码等必须使用安全随机源
- 普通算法随机和安全随机用途不同

### 面试回答要点

> 生成随机数通常依赖 PRNG，如 LCG、Xorshift；如果要求不重复，更像是采样或洗牌问题。若场景涉及安全令牌或密钥，必须用 CSPRNG，而不是普通伪随机算法。

---

## 9 如何实现一个非常简单的垃圾回收器？

最简单的 GC 模型通常从 **引用计数（Reference Counting）** 开始。

### 一个简单思路

- 每个对象维护引用计数
- 新引用产生时 `+1`
- 引用移除时 `-1`
- 当计数变成 `0` 时回收对象

### 一个极简 Python 示例

```python
class SimpleGC:
    def __init__(self):
        self.ref_count = {}

    def new_object(self, obj_id):
        self.ref_count[obj_id] = 1

    def add_ref(self, obj_id):
        self.ref_count[obj_id] += 1

    def release(self, obj_id):
        self.ref_count[obj_id] -= 1
        if self.ref_count[obj_id] == 0:
            print(f"collect {obj_id}")
            del self.ref_count[obj_id]
```

### 这个方案的优点

- 实现简单
- 回收时机明确
- 局部回收快

### 缺点

最大问题是 **无法处理循环引用**。

例如 A 引用 B，B 又引用 A，即使外部已经没人引用它们，计数也可能都不为 0。

### 更完整的 GC 通常会用

- mark-and-sweep
- generational GC
- tri-color marking
- compacting GC

### 面试回答要点

> 如果题目要求“简单 GC”，引用计数是最容易说明的方案；但要主动指出它无法处理循环引用，现代 GC 往往需要标记-清除或分代回收等机制补足这一点。

---

## 10 如何实现一个基础的消息 Broker？

一个最基础的 Broker，至少要支持：

- 发布
- 订阅
- 消息分发

### 极简内存版示例（Python）

```python
class Broker:
    def __init__(self):
        self.subscribers = {}

    def subscribe(self, topic, handler):
        self.subscribers.setdefault(topic, []).append(handler)

    def publish(self, topic, message):
        for handler in self.subscribers.get(topic, []):
            handler(message)


def print_handler(msg):
    print("received:", msg)


broker = Broker()
broker.subscribe("news", print_handler)
broker.publish("news", "hello")
```

### 但真正的消息系统要考虑很多额外问题

- 持久化
- ack / 重投
- 顺序保证
- 消费组
- 背压
- 死信队列
- 幂等
- 水平扩展

### 面试回答要点

> 一个最小 Broker 只需要 topic、subscriber registry 和分发逻辑；但真正可用的消息系统还要解决可靠性、顺序性、持久化和扩展性问题。

---

## 11 如何实现一个基础的 Web 服务器，并规划后续功能？

### 一个极简 Python HTTP 服务器

```python
from http.server import BaseHTTPRequestHandler, HTTPServer


class Handler(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.send_header("Content-Type", "text/plain; charset=utf-8")
        self.end_headers()
        self.wfile.write(b"Hello, World!")


if __name__ == "__main__":
    server = HTTPServer(("", 8000), Handler)
    print("listening on :8000")
    server.serve_forever()
```

### 最小可工作后，下一步通常补什么

#### 1. 路由
- 不同 path 映射不同 handler

#### 2. 请求解析
- query 参数
- header
- body
- JSON / form

#### 3. 并发处理
- 多线程 / 多进程 / event loop

#### 4. 静态文件与模板
- HTML / CSS / JS
- 模板渲染

#### 5. 日志和中间件
- access log
- request ID
- tracing
- auth

#### 6. 安全
- HTTPS
- 限流
- header 安全策略

### 面试回答要点

> 一个基础 Web 服务器可以先从 socket / HTTP request parsing / response writing 做起；而工业级 Web 服务器的价值主要体现在并发、安全、可观测性和扩展能力上。

---

## 12 如何对 10GB 文件排序？如果是 10TB 呢？

如果数据大到无法一次放进内存，就要用 **外部排序（external sort）**。

### 10GB 文件排序思路

假设内存只有 1GB：

1. 每次读入一块数据（例如 512MB 或 1GB）
2. 在内存中排序
3. 写回磁盘为多个有序临时文件
4. 对这些有序文件做多路归并
5. 输出最终结果

### 关键技术点

- 分块排序
- 多路归并
- 最小堆维护当前最小值
- 顺序 I/O 优于随机 I/O

### 10TB 怎么办

本质思路不变，只是规模更大：

- 更多临时文件
- 可能需要多层归并
- 可能需要分布式排序
- 更要重视磁盘吞吐、临时空间和失败恢复

### 现代工程补充

对 10TB 级别数据，常见会考虑：

- Hadoop / Spark sort
- 对象存储 + 分布式计算
- 按 key range 分区后并行排序

### 面试回答要点

> 大文件排序的核心是把“内存排序问题”变成“分块排序 + 多路归并”的外部排序问题。规模继续增大时，算法思想不变，但工程上会转向分布式执行和更强的失败恢复设计。

---

## 13 如何自动检测重复文件？

最常见的做法是分层过滤：

### 第一步：按文件大小分组

大小不同的文件一定不是重复文件。

### 第二步：按哈希值比较

对同尺寸文件计算内容哈希，例如：

- SHA-256
- BLAKE3

### 第三步：必要时做字节级确认

因为理论上哈希可能碰撞，严格场景下可做最终逐字节比对。

### 一个简单 Python 示例

```python
import hashlib
import os


def file_hash(path):
    h = hashlib.sha256()
    with open(path, "rb") as f:
        for chunk in iter(lambda: f.read(8192), b""):
            h.update(chunk)
    return h.hexdigest()


def find_duplicates(root):
    by_size = {}
    for dirpath, _, filenames in os.walk(root):
        for name in filenames:
            path = os.path.join(dirpath, name)
            size = os.path.getsize(path)
            by_size.setdefault(size, []).append(path)

    duplicates = []
    for _, files in by_size.items():
        if len(files) < 2:
            continue
        by_hash = {}
        for path in files:
            h = file_hash(path)
            by_hash.setdefault(h, []).append(path)
        for _, group in by_hash.items():
            if len(group) > 1:
                duplicates.append(group)

    return duplicates
```

### 更高级的扩展

- 增量扫描
- 内容分块指纹
- 相似文件检测（如图片感知哈希）
- 硬链接 / 去重存储

### 面试回答要点

> 检测重复文件最实用的方法是“先按大小筛，再按哈希比，再必要时逐字节确认”。这样能在正确性和效率之间取得较好平衡。
