1. [函数式语言是做什么的？什么时候我们需要使用函数语言？](#1-han-shu-shi-yu-yan-shi-zuo-shen-me-de-shen-me-shi-hou-wo-men-xu-yao-shi-yong-han-shu-yu-yan)
2. [Microsoft，Google，Opera和Mozilla公司从他们的浏览器中如何获利的？](#2-microsoftgoogleopera-he-mozilla-gong-si-cong-ta-men-de-liu-lan-qi-zhong-ru-he-huo-li-de)
3. [为什么打开TCP套接字有很大的开销？](#3-wei-shen-me-da-kai-tcp-tao-jie-zi-you-hen-da-de-kai-xiao)
4. [封装对于那些有重要的作用？](#4-feng-zhuang-dui-yu-na-xie-you-zhong-yao-de-zuo-yong)
5. [什么是实时系统？它和普通的系统有什么区别？](#5-shen-me-shi-shi-shi-xi-tong-ta-he-pu-tong-de-xi-tong-you-shen-me-qu-bie)
6. [实时语言(real-time language)和堆内存分配(heap memory allocation)之间的关系是什么？](#6-shi-shi-yu-yan-realtime-language-he-dui-nei-cun-fen-pei-heap-memory-allocation-zhi-jian-de-guan-xi-shi-shen-me)
7. [不可变性是怎么帮助我们提高编写更安全的代码？](#7-bu-ke-bian-xing-shi-zen-me-bang-zhu-wo-men-ti-gao-bian-xie-geng-an-quan-de-dai-ma)
8. [可变性变量和不可变量有什么优势和弊端？](#8-ke-bian-xing-bian-liang-he-bu-ke-bian-liang-you-shen-me-you-shi-he-bi-duan)
9. [什么是O/R阻抗失衡(Object-Relational impedence mismatch)？](#9-shen-me-shi-or-zu-kang-shi-heng-objectrelational-impedence-mismatch)
10. [缓存大小在设计的时候需要考虑哪些原则？](#10-huan-cun-da-xiao-zai-she-ji-de-shi-hou-xu-yao-kao-lv-na-xie-yuan-ze)
11. [客户端渲染和服务端渲染有什么各自弊端，如何取舍？](#11-ke-hu-duan-xuan-ran-he-fu-wu-duan-xuan-ran-you-shen-me-ge-zi-bi-duan-ru-he-qu-she)
12. [如何在不可靠的协议上开发出可靠通讯协议？](#12-ru-he-zai-bu-ke-kao-de-xie-yi-shang-kai-fa-chu-ke-kao-tong-xun-xie-yi)
13. [想象一下如果在你最喜欢的语言移除空引用的问题，你该如何做？会导致什么样的后果？](#13-xiang-xiang-yi-xia-ru-guo-zai-ni-zui-xi-huan-de-yu-yan-yi-chu-kong-yin-yong-de-wen-ti-ni-gai-ru-he-zuo-hui-dao-zhi-shen-me-yang-de-hou-guo)

## 1 函数式语言是做什么的？什么时候我们需要使用函数语言？
函数式语言是一种编程范式，在函数式语言程序是由调用和组合函数而成。这是一种声明式编程式编程语言，是由一系列表达式构成的树组成，通常将一些值转换成其他值。
在函数式编程中，函数被认为是第一等公民，也就意味着它可以和一个变量绑定，作为参数传递到其他函数中，或者从其他函数中返回。
当在函数式语言中，如果所有的函数都是类似数学函数，或者纯函数，也就是说对于任何相同的输入，它的返回值都是一样的，而不会影响任何其他可变的状态或者有其他副作用，那么我们可以叫做纯函数编程。纯函数编程通常有更少的 bug, 非常容易调试和测试。

函数式语言起源于学术界，因此它非常它在编程语言理论研究中广泛应用。函数式语言特别适用于一些对于同一个数据集进行多次操作的场景中，比如机器学习。函数式语言在金融领域的风险控制中也广泛使用，因为每个函数都可以看做关系图中的一个节点。
## 2 Microsoft，Google，Opera和Mozilla公司从他们的浏览器中如何获利的？

在上个世纪的 90 年代，网景公司（netscape）发布一款浏览器叫做 `Netscape Navigator`，该软件风靡全球。这时微软觉得这款软件威胁到 `Windows` 在桌面操作系统的统治地位。于是微软开发出了自己的浏览器 `Internet Explorer`，该软件拥有和 `Netscape Navigator` 同样的功能，最致命的是该软件采用的免费的策略，可以和 `Windows` 操作系统深度绑定。因此在这场浏览器大战中，微软的 `IE` 浏览器笑到了最后。虽然微软没有从浏览器中没有挣到钱，但是通过与 `Windows` 系统深度绑定免费策略，巩固了微软在桌面领域的统治地位。

在微软赢得浏览器大战之后，并没有将更多的资源放在浏览器上。在网景公司倒闭后，成立了 Mozilla 公司，在 2004 年发布了 `firefox` 浏览器。由于插件的机制，该浏览器受欢迎的程度在 2009 年就超过了 `IE` 浏览器。那么 Mozilla 是如何通过浏览器盈利的呢？通过该公司的年度财报我们可以发现其 `95%` 的收益来自于特许权，主要是 `firefox` 浏览器的默认搜索引擎的设置。在 `2014` 年之前，`Mizilla` 于 `google` 达成协议，使用 `google` 作为默认搜索引擎；在 `2014` 到 `2017`, 于 `Yahoo` 达成协议，切换为 `Yahoo` 的搜索引擎；后来继续使用 `google` 搜索引擎。

在 2008 年，`google` 发布了 `Chrome` 浏览器。这是一款一鸣惊人的浏览器，并且在很短的时间内统治了浏览器市场。由于 `Chrome` 的默认的搜索引擎就是 `google`, 因此 `google` 不需要向别的浏览器付费来设置默认浏览器。除此之外，人们在使用 `google` 浏览器的时候，通常也会使用 `gmail`, `google apps` , `google docs` 等服务，这些都会增加 `google` 的收入。还有 google 的 `adsense` 计划会使用 Chrome 来记录用户的数据。更多的数据会有助于更好的市场推广和广告投放。

## 3 为什么打开TCP套接字有很大的开销？
*todo*
## 4 封装对于那些有重要的作用？
*todo*
## 5 什么是实时系统？它和普通的系统有什么区别？
*todo*
## 6 实时语言(real-time language)和堆内存分配(heap memory allocation)之间的关系是什么？
*todo*
## 7 不可变性是怎么帮助我们提高编写更安全的代码？
*todo*
## 8 可变性变量和不可变量有什么优势和弊端？
*todo*
## 9 什么是O/R阻抗失衡(Object-Relational impedence mismatch)？
*todo*
## 10 缓存大小在设计的时候需要考虑哪些原则？
*todo*
## 11 客户端渲染和服务端渲染有什么各自弊端，如何取舍？
*todo*
## 12 如何在不可靠的协议上开发出可靠通讯协议？
*todo*
## 13 想象一下如果在你最喜欢的语言移除空引用的问题，你该如何做？会导致什么样的后果？
*todo*