## 1 说一下你最喜欢语言的三个缺陷

C# 语言

1. 开源太晚

虽然说现在 `C#` 已经开源，但是面对互联网，云计算和大数据时代还是显得有点太晚了。在一些技术社区仍然以为 C# 知识 Windows Only 的开发语言。这个对于新的开发者而言是一个很错误的引导，而且吸引不了更多的开发者进入这个行业。而且在过去几年，C# 开发领域由很多令人困惑的概念，比如说 `.Net Core`, `.Net Standard`, `Mono`, `.Net 5` 以及传统的 `.Net Framework`。这些概念对于有经验的开发工程师都难以区分它们。

2. 复杂的比较操作

在 C# 中有很多比较操作，这些操作往往令开发者难以区分。

- 用户自定一个比较操作： `>`, `<`, `>=`,`==`,`!=`等等
- 重载 `Equals(object)` 这个方法
- `Object` 类中包含的 `Equals` 这个静态方法
- `IComparable` 接口
- `IEquality` 接口

3. 对接口限制太严格

对于接口，只能包含了方法和属性，不能包含字段，静态方法等等。

## 2 为什么现在对函数式编程语言越来越受到欢迎？

大部分应用程序在开发的过程中的缺陷主要是由软件开发者并没有完整的清楚代码在实际运行时候全部的状态。
尤其是在多线程运行环境中，这个问题就会被放大。通过函数式编程软件中所有的状态就会变得明确，同样使得
诸如多线程的条件竞争等问题得到解决。纯函数是函数式编程重要的内容，它只关注传递给他的参数，返回根据
传入的参数计算而得的值，没有逻辑上的副作用(`side effect`)。它不更新全局变量，不维持全局变量，
也不会进行IO操作，更不会修改传入的参数。纯函数的有一下几点优势

- 线程安全：纯函数只使用参数，所以它是完全线程安全的的；所以很容易地将这些函数改造成并行执行，尤其在多核CPU中发挥优势；
- 可重用性：将纯函数转移到新的环境非常简单，只需要处理类型定义和函数调用，不会发生类似滚雪球效应；
- 可测试性：纯函数是引用透明的，也就是说同样的参数调用无论如何都会返回正确的结果；
- 可理解性和可维护性：只关心参数的输入和结果的输出，大大降低了维护者的理解难度

## 3 什么是闭包，闭包有什么作用？它和类有什么区别？

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

## 4 什么是高阶函数？它是用来做什么的？用你最喜欢的语言写一个高阶函数;

如何一个函数接受另一个函数作为参数或者返回函数，那么这个函数就是高阶函数。
高阶函数能够表达出更强的抽象。

```go
func twice(f func(int) int, v int) int {
	return f(f(v))
}

func main() {
	f := func(v int) int {
		return v + 3
	}
	twice(f, 7) // returns 13
}
```

## 5 编写一个循环，然后将它转换成递归的形式，并且只能使用不可变结构（比如避免使用变量）

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

## 6 什么是栈和堆？什么叫栈溢出？

由于虚拟内存的设计，每一个应用程序 "仿佛" 使用了全部机器的内存，一般来讲程序内存划分情况如下图:

![内存](images/memory.png)

- 地址 `0xffffffff - 0xc0000000` 为内核地址；
- 地址 `0x08048000` 往上为程序的只读段，主要包含了代码段，只读数据段，再往上为数据段；
- 再往上为堆，所有程序中手动分配的内存将在这个位置开始往上分配；
- 地址 `0x40000000` 往上一部分为动态共享库；
- 地址 `0xc0000000` 往下为栈空间。

操作系统为为每一个函数调用提供了栈帧，主要保存函数的参数、返回地址和一些局部变量。如果程序设计不当，将会导致栈帧使用完毕，导致栈溢出，常见的主要有无限递归。

## 7 命名空间（namespace)是做什么的？能够发明一个可替代性的东西？

在编程领域中，命令空间主要解决变量，函数以及类它们之间的冲突。假设你的应用程序使用了两个库。

```C#
// library A 
public class FooBar 
{
    //...
}

// library B
public class FooBar
{
    //...
}
```
我们可以看到，`FooBar` 两个类出现了两个库，我们的应用程序编译器不能区分它们，所以我们引入了命名空间。

```C#
// libray A
namespace Tindo.SDK
{
    public class FooBar {}
}

// library B
namespace Aurisoft.Tool
{
    public class FooBar {}
}
```

现在我们就能很好的区分它们，不会发生对象解析错误。

如果我们能够解析冲突，就不需要命令空间。我们可以为每个库的对象能唯一值标记即可。

```C#
// libaray A -> libraryA.dll
public class FooBar {}

// library B -> libraryB.dll
public class FooBar {}


// programa
using FooBarA = import("libraryA.dll", "FooBar");
using FooBarB = import("libraryB.dll", "FooBar");

```

## 8 编写两个函数，一个是引用透明（`Referentially Transparent`)，另一个是引用不透明（`Referentially Opaque`）

首先什么是引用透明呢? 它用来描述定义一个表达式的事实，在一个程序中，如果一个表达式可以被一个具体的值取代而不影响结果那么我们就可以称为改引用透明，从某种程度来讲就是改表达式由特定的参数输入一定会输出相同的结果，这是函数式编程的概念。

假设我们由下面几个函数

```C#
int Add(int a, int b){
    return a + b;
}

int Mult(int a, int b){
    return a * b;
}

int x = Add(2, Mult(3, 4));
```

在上面的例子中， `Mult` 函数就是引用透明的，因为我们可以用 `12` 替换掉 `Mult(3, 4)` 而不会有任何影响；同样我们也可以用 `14` 替换 `Add(2, 12)`。

下面再介绍一下引用不透明的例子 

```C#
int Add(int a, int b){
    int result = a + b;
    Console.WriteLine($"Returning {result}");
    return result;
}
```

如果我们用特定的值替换 `Add` 方法，那么 `Returning` 方法就不会输出，产生了副作用 (Side Effect）。有些情况下，非但带来了副作用，而且导致的结果也不正确。

```C#
class Fibs {
    private int previous = 1;
    private int last = 1;

    public int Next() {
        last = previous + (previous = last);
        return prevous + last;
    }
}

public void PrintFibs(int limit){
    Fibs fibs = new Fibs();
    for(int i =0; i < limit; i++){
        Console.WriteLine(fibs.Next());
    }
}
```

在这里我们不能用任何值代替 `Next` 方法的调用，因为这个方法在每次调用的时候就是不一样的。


## 9 为什么在有些语言设计中没有异常机制？那么它们有什么优势和弊端？

异常的设计是随着语言的发展而发展的，在早期的语言，比如汇编语言并没有应用程序层面的异常，只需要顺序和跳转两中执行控制语句就可以完成全部的工作。现代语言通常封装了底层的逻辑，因此也提供了大量的高级的语言的特性，所以异常自然而然提出。

**优势** 
- 异常可以将错误处理代码和正常的逻辑流区分开来，这样代码就可以很容易的阅读，健壮和可拓展性

举个例子如下

使用异常处理
```c++
// sample 1: A function that uses exceptions
string get_html(const char* url, int port)
{
    Socket client(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    client.connect(url, port);
    
    stringstream request_stream;
    request_stream << "GET / HTTP/1.1\r\nHost: " 
       << url << "\r\nConnection: Close\r\n\r\n";

    client.send(request_stream.str());

    return client.receive();
}
```

如果使用错误代码

```c++
// sample 2: A function that uses error codes
Socket::Err_code get_html(const char* url, int port, string* result)
{
    Socket client;
    Socket::Err_code err = client.init(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    if (err) return err;
        
    err = client.connect(url, port);
    if (err) return err;
    
    stringstream request_stream;
    request_stream << "GET / HTTP/1.1\r\nHost: " << url 
       << "\r\nConnection: Close\r\n\r\n";

    err = client.send(request_stream.str());
    if (err) return err;

    return client.receive(result);
}
```

上面的两个例子都是完成同样的事情，但是从错误处理的版本来看，代码需要处理很多错误的情况，使代码的可读性不高。

- 只有抛出异常才能解决构造函数的的错误

在类的构造函数中，通常需要申请一些系统资源，如果申请失败，就会让对象处于不稳定的状态。如果使用错误处理就不能处理这种情况。

- 异常很难被忽略

对于没有捕获的异常，系统就会 crash 掉，这个有助于系统维护者更早的发现发现问题，解决问题，而不是忽略它们。但是对于错误处理这种方式，就很难做到。

- 异常可以从嵌套的函数中传播出来

使用异常可以很方便地将错误从发生地地方到最外面调用地地方。

- 异常可以使用自定义地类型，它们可以比错误代码包含更多地信息

通常错误代码使用整型，而且没有更多的信息。当然可以为错误代码设计为一个 Object，但是需要复制很多次这种对象。但是异常的话，本身就是一个对象，而且可以通过类型系统来处理它们。

```c++
// Exception  handler

void AppDialog::on_button()
{
    try {
        string url = url_text_control.get_text();
        result_pane.set_text(
            get_title(url));
    }
    catch(Socket::SocketConnectionException& sock_conn_exc) {
        display_network_connection_error_message();
    }
    catch(Socket::Exception& sock_exc) {
        display_general_network_error_message();
    }
    catch(Parser::Exception& pars_exc) {
        display_parser_errorMessage();
    }
    catch(...) {
        display_unknown_error_message();
    }
}
```

通过异常类型的条件，处理不同的情况。

**劣势**

- 异常为代码逻辑增加了很多不可见的退出点，这样的增加的代码检查的难度。

以为异常可以跳出正在正在执行的逻辑代码流，所以在无形之中为代码函数增加了退出的机制

- 异常可能导致资源泄露，尤其使没有内置垃圾回收的编程语言

由于异常可以提前退出整个代码逻辑，所以可能导致已经分配系统资源的没有执行释放代码。

- 异常的发生会导致性能上的损失

众所周知，异常对系统的性能是由损失的。

## 10 为什么在JAVA，或者C#中，构造函数不是接口的一部分？

构造函数是特殊的成员函数方法用来初始化新创建的对象，它会在类对象创建的时候自动被调用。但是构造函数并不是接口的一部分。

- 接口是类的完全的抽象，在 Java 中接口中的所有的数据成员都是默认 `public`, `static` 并且 `final` 修饰的。所有的静态字段必须在声明的时候就应当赋值，否则就会出现编译的时候错误。

- 接口中的方法都是默认 `public` 的，而且也是 `abstract` 这就意味着在接口中不应当提供具体的实现，应当由实现接口的类来完成这部分工作。因此，没有必要再接口中包含一个构造方法。

- 构造函数用来初始化非静态的数据成员，因为在接口中没有非静态的数据成员，所以没有构造函数的必要。

- 接口中的方法只有声明没有定义，由于没有方法的具体实现，所以没有必要有一个对象来调用方法同样也不会有构造函数。