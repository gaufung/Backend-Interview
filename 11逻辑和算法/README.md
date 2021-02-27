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
*todo*
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

