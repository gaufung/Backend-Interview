
1. [为什么在SOA中，长时间事务是不推荐的，而是使用Sagas?](#1-wei-shen-me-zai-soa-zhong-chang-shi-jian-shi-wu-shi-bu-tui-jian-de-er-shi-shi-yong-sagas)
2. [Soa和微服务（microservice)有什么区别？](#2-soa-he-wei-fu-wu-microservice-you-shen-me-qu-bie)
3. [web服务如何进行版本管理，版本兼容和打破改变？](#3-web-fu-wu-ru-he-jin-hang-ban-ben-guan-li-ban-ben-jian-rong-he-da-po-gai-bian)
4. [事务和saga在SOA中有什么区别？](#4-shi-wu-he-saga-zai-soa-zhong-you-shen-me-qu-bie)
5. [什么使用微服务显得太微（too micro)了?](#5-shen-me-shi-yong-wei-fu-wu-xian-de-tai-wei-too-micro-le)
6. [微服务架构的优缺点是什么？](#6-wei-fu-wu-jia-gou-de-you-que-dian-shi-shen-me)

## 1 为什么在SOA中，长时间事务是不推荐的，而是使用Sagas?
## 2 Soa和微服务（microservice)有什么区别？
## 3 web服务如何进行版本管理，版本兼容和打破改变？
## 4 事务和saga在SOA中有什么区别？
## 5 什么使用微服务显得太微（too micro)了?

## 6 微服务架构的优缺点是什么？

微服务架构（Microservice Architecture) 有如下的优缺点：
优点：
1. 提高错误隔离能力：如果说某个单模块发生了故障，应用程序或者服务仍然不受影响
2. 避免技术限制：微服务提供很灵活的技术栈选择，因为使用微服务没有依赖的限制，因此可以选择更加先进的技术。
3. 容易理解：通过拆分应用程序的模块，开发人员可以很清楚的理解服务的功能。
4. 快速迭代：更小的代码意味着开发速度更快，这样可以使用持续集成和部署快读迭代各个模块。
5. 可扩展性：由于各个服务已经拆分了，这样可以扩展最需要的模块，提高应用程序或者服务的性能。

缺点：
1. 服务之间通信变得复杂：由于每个服务之间都是独立的，所有需要特别小心地处理服务之间的请求，随着服务的增加，这个复杂度是指数增加的。而且通过远程调用，会增加延迟。
2. 消耗更多的资源：更多的微服务会增加 `CPU`， 内存和带宽的使用
3. 全局测试变得困难：测试微服务变得有点困难，因为需要确保多有依赖的微服务都在正常工作。
4. 部署的挑战：在部署的时候，需要不同的服务之间协同工作才能保证正确部署。
