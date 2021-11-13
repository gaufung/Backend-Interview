1. [什么是敏捷？](#1-shen-me-shi-min-jie)
2. [你是如何处理历史遗留代码？](#2-ni-shi-ru-he-chu-li-li-shi-yi-liu-dai-ma)
3. [假设我是项目经理，并且没有编程经验，那么你能跟我解释历史代码并且告诉我为什么关注代码质量？](#3-jia-she-wo-shi-xiang-mu-jing-li-bing-qie-mei-you-bian-cheng-jing-yan-na-me-ni-neng-gen-wo-jie-shi-li-shi-dai-ma-bing-qie-gao-su-wo-wei-shen-me-guan-zhu-dai-ma-zhi-liang)
4. [如果我是公司的CEO，那么向我解释Kanban，并且说服我在上面投资；](#4-ru-guo-wo-shi-gong-si-de-ceo-na-me-xiang-wo-jie-shi-kanban-bing-qie-shuo-fu-wo-zai-shang-mian-tou-zi)
5. [敏捷和瀑布流最大的区别是什么？](#5-min-jie-he-pu-bu-liu-zui-da-de-qu-bie-shi-shen-me)
6. [作为一个团队管理者，你是如何处理有太多的会需要参加的问题？](#6-zuo-wei-yi-ge-tuan-dui-guan-li-zhe-ni-shi-ru-he-chu-li-you-tai-duo-de-hui-xu-yao-can-jia-de-wen-ti)
7. [你是如何处理延期的项目？](#7-ni-shi-ru-he-chu-li-yan-qi-de-xiang-mu)
8. ["个体与交互重于过程和工具"和"客户协作重于合同谈判"占了敏捷宣言（Agile Manifesto）的一半，谈论一下这两个观念；](#8-ge-ti-yu-jiao-hu-zhong-yu-guo-cheng-he-gong-ju-he-ke-hu-xie-zuo-zhong-yu-he-tong-tan-pan-zhan-le-min-jie-xuan-yan-agile-manifesto-de-yi-ban-tan-lun-yi-xia-zhe-liang-ge-guan-nian)
9. [如果你是公司的CTO，那么你会采取什么措施？](#9-ru-guo-ni-shi-gong-si-de-cto-na-me-ni-hui-cai-qu-shen-me-cuo-shi)
10. [项目经理有用吗？](#10-xiang-mu-jing-li-you-yong-ma)
11. [如果要你组织一个弹性工作制的开发团队（即没有强制工作时间的要求），并且假期制度是"按需休假"，你会如何做？](#11-ru-guo-yao-ni-zu-zhi-yi-ge-tan-xing-gong-zuo-zhi-de-kai-fa-tuan-dui-ji-mei-you-qiang-zhi-gong-zuo-shi-jian-de-yao-qiu-bing-qie-jia-qi-zhi-du-shi-an-xu-xiu-jia-ni-hui-ru-he-zuo)
12. [你会如何管理一个人员流动非常高的团队？如何在不加薪的条件下说服团队成员不要离开？](#12-ni-hui-ru-he-guan-li-yi-ge-ren-yuan-liu-dong-fei-chang-gao-de-tuan-dui-ru-he-zai-bu-jia-xin-de-tiao-jian-xia-shuo-fu-tuan-dui-cheng-yuan-bu-yao-li-kai)
13. [除了代码之外，你认为你要找的同事最重要的三个特质是什么？](#13-chu-le-dai-ma-zhi-wai-ni-ren-wei-ni-yao-zhao-de-tong-shi-zui-zhong-yao-de-san-ge-te-zhi-shi-shen-me)
14. [对于非技术背景的人，你认为三个最重要的事情是什么？](#14-dui-yu-fei-ji-shu-bei-jing-de-ren-ni-ren-wei-san-ge-zui-zhong-yao-de-shi-qing-shi-shen-me)
15. [如果公司给你一个月时间和一些预算来提高你同事的日常生活，你会怎么做？](#15-ru-guo-gong-si-gei-ni-yi-ge-yue-shi-jian-he-yi-xie-yu-suan-lai-ti-gao-ni-tong-shi-de-ri-chang-sheng-huo-ni-hui-zen-me-zuo)

## 1 什么是敏捷？
在软件开发领域，敏捷意味着 
- 快速有效地应对改变，并且在团队有效地沟通
- 敏捷要求工作是基于人，而不是计划
- 敏捷要求开发团队专注于软件本身，而不是设计和文档
- 敏捷相信迭代的方法
- 敏捷的目标是快速的将产品交付给客户。

在敏捷开发的注意点

1. 计划
- 计划开始于创建一些列 Story，它们包含软件所需要的功能
- Story 是有客户创建，客户将 Story 的价值和商业价值联系起来
- 团队的每个成员在每周都要评估相应的 Story
- 如果一个 Story 需要超出 3 周的时间，需要将它们继续拆分
- 客户和开发人员需要将一系列 story 合并起来，并将它们放到下一个 release 中
- 是基于 release 进行保证交付

2. 设计
- 设计要基于 KIS (Keep it simple) 原则，简单的设计远远好于复杂的设计
- 需要为 Story 提供的实现设计文档
- 鼓励重构

3. 编码
- 当 Story 和设计完成后，并不与要着急编写代码，而是谢谢一些列期待行为的单元测试
- 一旦单元测试完成，开发者需要专注于让单元测试通过
- 一旦代码完成，就可以直接运行单元测试，这样可以提供及时反馈
- 可以采用结对编程，这样可以保证一个专注于修复现实问题，另一个专注于代码质量
- 一旦结对编程完成，代码就可以和其他团队一起集成
- 持续继承可以避免兼容性问题，也可以通过冒烟测试发现未知的错误。

4. 测试
- 单元测试是优先创建
- 单元测试应当使用框架，可以可以自动化执行
- 单个单元测试需要拼装成特定的套件
- 接受客户测试，用来判断是否完成原先的需求。

## 2 你是如何处理历史遗留代码？
*todo*
## 3 假设我是项目经理，并且没有编程经验，那么你能跟我解释历史代码并且告诉我为什么关注代码质量？
*todo*
## 4 如果我是公司的CEO，那么向我解释Kanban，并且说服我在上面投资；
*todo*
## 5 敏捷和瀑布流最大的区别是什么？
*todo*
## 6 作为一个团队管理者，你是如何处理有太多的会需要参加的问题？
*todo*
## 7 你是如何处理延期的项目？
*todo*
## 8 "个体与交互重于过程和工具"和"客户协作重于合同谈判"占了敏捷宣言（Agile Manifesto）的一半，谈论一下这两个观念；
*todo*
## 9 如果你是公司的CTO，那么你会采取什么措施？
*todo*
## 10 项目经理有用吗？
*todo*
## 11 如果要你组织一个弹性工作制的开发团队（即没有强制工作时间的要求），并且假期制度是"按需休假"，你会如何做？
*todo*
## 12 你会如何管理一个人员流动非常高的团队？如何在不加薪的条件下说服团队成员不要离开？
*todo*
## 13 除了代码之外，你认为你要找的同事最重要的三个特质是什么？

1. Debug 能力

`Debug` 是一项重要的能力，因为在软件开发中，肯定会遇到 `Bug`，那么如何将它们消灭是工作的一部分。`Debug` 过程如下：

- 复现 bug
- 梳理代码逻辑
- 修复 bug 
- 添加测试，包含单元测试和功能测试
- 添加文档

这个完整的流程对于软件的业务逻辑将会有更加深刻的理解。

2. 阅读文档能力

在软件开发过程中会使用很多第三方的库，通常这些库会包含文档。软件开发人员一个很重要的工作是通过这些文档来判断该库是否满足业务开发的需求。而且对于第三方库，通过阅读文档可以完整地了解它的正确的使用方式。

3. 技术输出能力

对于一个技术的掌握程度是这样排序的

- 观看视频
- 阅读文档
- 亲手实践
- 教会他人

因此通过教会他人才会让你真正掌握一项技术，教会他人就是技术输出能力。这样的形式有多种多样，比如博客，播客或者是视频。


## 14 对于非技术背景的人，你认为三个最重要的事情是什么？
*todo*
## 15 如果公司给你一个月时间和一些预算来提高你同事的日常生活，你会怎么做？
*todo*