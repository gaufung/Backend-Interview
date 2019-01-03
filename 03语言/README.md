# 什么是闭包，闭包有什么作用？它和类有什么区别？
闭包（Closure）是词法闭包（Lexical Closure）的简称，闭包提供了一种方位内部变量的一种方式。
程序设计中，每一个变量都有一定的作用域，作用域之外的将不能访问该该变量
```go
var a = 1

func func1() {
    var b = 10
    fmt.Printf("%d", a)
}

// error
func func2(){
    fmt.Printf("%d", b)
}
```
变量`a`是全局变量，所以对`func1`和`func2`都可见，但是变量`b`是局部变量，对于`func2`是不可见的，所以无法访问`b`。这是由`go`语言的"链式作用域"结构（`chain scope`）决定的。子对象会一级一级地向上寻找所有父对象的变量，所以，父对象的所有变量，对子对象都是可见的，反之则不成立。
但是闭包提供了方位局部变量的方法：
```go
func func3() func() {
    var c = 10
    return func(){
        c++
        fmt.Printf("%d", c)
    }
}
handler := func3()
handler() // 11
handler() // 12 
```
在`go`语言中，函数是一等公民(`first class citizen`)，所以`func3`可以返回一个函数。该函数包含了局部变量`c`，所以在外面就可以访问`c`变量的方式。
使用闭包的可以减少变量的使用，使用局部变量就可以保存全部的状态。


# 编写一个循环，然后将它转换成递归的形式，并且只能使用不可变结构（比如避免使用变量）
```go
func factorialInter(n int) int {
    val := 1
    for i:=1; i<n; i++ {
        val = val * i
    }
    return val
}

func factorialRec(n int, val int) int {
    if n = 1 {
        return val
    }else{
        return factorialRec(n-1, val*n)
    }
}
```