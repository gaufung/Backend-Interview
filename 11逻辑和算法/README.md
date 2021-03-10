1. [仅仅使用LIFO栈来实现FIFO的队列，然后使用FIFO的队列来实现FIFO的栈](#1-jin-jin-shi-yong-lifo-zhan-lai-shi-xian-fifo-de-dui-lie-ran-hou-shi-yong-fifo-de-dui-lie-lai-shi-xian-fifo-de-zhan)
2. [使用代码片段来实现栈溢出](#2-shi-yong-dai-ma-pian-duan-lai-shi-xian-zhan-yi-chu)
3. [使用尾递归版本的Fraction方法](#3-shi-yong-wei-di-gui-ban-ben-de-fraction-fang-fa)
4. [使用你最熟悉的语言，来实现一个REPL，它将输出任何输出；执行RPN表达式](#4-shi-yong-ni-zui-shou-xi-de-yu-yan-lai-shi-xian-yi-ge-repl-ta-jiang-shu-chu-ren-he-shu-chu-zhi-hang-rpn-biao-da-shi)
5. [如何设计一个磁盘整理碎片工具？](#5-ru-he-she-ji-yi-ge-ci-pan-zheng-li-sui-pian-gong-ju)
6. [编写一个随机生成迷宫的程序](#6-bian-xie-yi-ge-sui-ji-sheng-cheng-mi-gong-de-cheng-xu)
7. [编写一个实例代码能够导致内存泄漏](#7-bian-xie-yi-ge-shi-li-dai-ma-neng-gou-dao-zhi-nei-cun-xie-lou)
8. [生成一系列不同的随机数](#8-sheng-cheng-yi-xi-lie-bu-tong-de-sui-ji-shu)
9. [编写简单的垃圾回收系统](#9-bian-xie-jian-dan-de-la-ji-hui-shou-xi-tong)
10. [编写基础的消息发送broker](#10-bian-xie-ji-chu-de-xiao-xi-fa-song-broker)
11. [编写基础的web服务器，并且绘制出将来的要完成的功能](#11-bian-xie-ji-chu-de-web-fu-wu-qi-bing-qie-hui-zhi-chu-jiang-lai-de-yao-wan-cheng-de-gong-neng)
12. [如何对10GB的文件排序，那么10TB文件如何呢？](#12-ru-he-dui-10-gb-de-wen-jian-pai-xu-na-me-10-tb-wen-jian-ru-he-ne)
13. [如何自动检测冗余的文件？](#13-ru-he-zi-dong-jian-ce-rong-yu-de-wen-jian)

## 1 仅仅使用`LIFO`栈来实现`FIFO`的队列，然后使用`FIFO`的队列来实现`FIFO`的栈
  
```go
// Using two stacks to implement queue
type Queue struct {
    inStack Stack
    outStack Stack
}
func (q *Queue) Enqueue(item interface{}){
    for val, err:= q.outStack.Pop(); err==nil {
        q.inStack.Push(val)
    }
    q.inStack.Push(val)
}
func (q *Queue) Dequeue()(interface{}, error){
    for val, err := q.inStack.Pop(); err ==nil{
        q.outStack.Push(val)
    }
    return q.outStack.Pop()
}
// Using two queues to implement stack
type Stack struct{
    mainQueue Queue
    backupQueue Queue
}
func (s *Stack) Push(item interface{}){
    s.mainQueue.Enqueue(item)
}
func (s *Stack) Pop()(interface{}, error){
    var val interface{}
    err := errors.News("empty stack")
    for v, err := s.mainQueue.Dequeue(); err == nil {
        val = v
        s.backupQueue.Enqueue(v)
    }
    // switch queues
    s.backupQueue, s.mainQueue = s.mainQueue, s.backupQueue
    return val, err
}

```

## 2 使用代码片段来实现栈溢出
对于递归，如果没有递归基，也就是递归的出口。那么就会导致栈溢出。

```C#
public int Fib(n)
{
    return Fib(n-1) + Fib(n-2);
}
```

## 3 使用尾递归版本的Fraction方法
*todo*
## 4 使用你最熟悉的语言，来实现一个REPL，它将输出任何输出；执行RPN表达式
*todo*

## 5 如何设计一个磁盘整理碎片工具？
*todo*

## 6 编写一个随机生成迷宫的程序
*todo*

## 7 编写一个实例代码能够导致内存泄漏
*todo*

## 8 生成一系列不同的随机数
*todo*

## 9 编写简单的垃圾回收系统
*todo*

## 10 编写基础的消息发送broker
*todo*

## 11 编写基础的web服务器，并且绘制出将来的要完成的功能
*todo*

## 12 如何对10GB的文件排序，那么10TB文件如何呢？
*todo*
## 13 如何自动检测冗余的文件？
*todo*

