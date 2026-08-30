# 后端开发者面试问题

> 一份面向现代后端工程师的中文面试题库与知识地图。  
> 覆盖设计模式、系统设计、数据库、并发、分布式系统、安全、架构、工程效能与团队协作。

## 这是什么

这个仓库最初源自经典的后端面试问题整理，现在已经完成一轮**内容现代化重构**，目标不是只保留“题目”，而是把它升级为一份更贴近当代行业实践的学习资料。

你可以把它当成：

- 后端面试准备清单
- 系统设计与工程实践知识索引
- 团队内部学习分享材料
- 校准技术判断与工程权衡的参考手册

## 适合谁

- 准备后端 / 平台 / 基础架构岗位面试的工程师
- 想系统回顾后端知识体系的开发者
- 想把“会做题”升级为“会做工程判断”的同学
- 需要组织团队学习、技术分享或培训材料的 Tech Lead / Manager

## 这次重构做了什么

本仓库已经完成全章节现代化整理，重点包括：

- 修正过时、不准确或过于绝对化的表述
- 用更现代的工程语境重写答案
- 强化**权衡（trade-off）**而不是“标准答案”思维
- 增补云原生、可观测性、API 治理、平台工程、DevSecOps 等视角
- 统一章节结构、术语、代码示例风格和表达质量
- 让答案更适合真实面试中的结构化表达

详细过程见：[MODERNIZATION_PLAN.md](./MODERNIZATION_PLAN.md)

## 你会看到的内容风格

和传统题库相比，这一版更强调：

- **是什么**：概念定义
- **为什么**：设计动机
- **适合什么场景**：上下文判断
- **代价与边界**：工程现实
- **面试怎么答**：结构化表达

换句话说，这不是单纯背八股，而是帮助你形成更成熟的工程判断。

## 阅读建议

如果你是第一次看，推荐按下面顺序：

### 路线 A：面试冲刺
1. [代码设计](./02代码设计/README.md)
2. [Web 开发](./04Web开发/README.md)
3. [数据库](./05数据库/README.md)
4. [并发](./08并发/README.md)
5. [分布式系统](./09分布式系统/README.md)
6. [软件架构](./12软件架构/README.md)
7. [安全](./14安全/README.md)

### 路线 B：系统补课
1. [关于设计模式](./01关于设计模式/README.md)
2. [语言](./03语言/README.md)
3. [NoSQL](./06NoSQL/README.md)
4. [SOA 和 Microservices](./13SOA和Microservices/README.md)
5. [通用问题](./15通用问题/README.md)
6. [开放问题](./16开放问题/README.md)

## 全部目录

### [1 关于设计模式](./01关于设计模式/README.md)
### [2 代码设计](./02代码设计/README.md)
### [3 语言](./03语言/README.md)
### [4 Web 开发](./04Web开发/README.md)
### [5 数据库](./05数据库/README.md)
### [6 NoSQL](./06NoSQL/README.md)
### [7 代码版本管理](./07代码版本管理/README.md)
### [8 并发](./08并发/README.md)
### [9 分布式系统](./09分布式系统/README.md)
### [10 软件生命周期和团队管理](./10软件生命周期和团队管理/README.md)
### [11 逻辑和算法](./11逻辑和算法/README.md)
### [12 软件架构](./12软件架构/README.md)
### [13 SOA 和 Microservices](./13SOA和Microservices/README.md)
### [14 安全](./14安全/README.md)
### [15 通用问题](./15通用问题/README.md)
### [16 开放问题](./16开放问题/README.md)
### [17 Bill Gates 问题](./17BillGates问题/README.md)

## 当前状态

- [x] 根目录说明已更新
- [x] 17 个章节 README 已完成现代化重构
- [x] 章节标题、术语、结构风格已统一
- [x] 面试表达导向已增强

## 项目来源

- GitBook： [后端程序员面试问题集锦](https://fungkao.gitbook.io/backendinterview/)
- 英文原版： [Backend developer interview questions](https://github.com/arialdomartini/Back-End-Developer-Interview-Questions)
- 中文作者： [高峰](https://gaufung.github.com) (gaufung@outlook.com)
- GitHub： [Backend Interview](https://github.com/gaufung/Backend-Interview)
- 推荐使用 [Typora](https://www.typora.io) 或 GitBook 阅读

## 如何使用这个仓库

你可以按三种方式使用它：

1. **按章节系统学习**：适合补全知识图谱
2. **按问题跳读**：适合面试前查漏补缺
3. **做团队讨论提纲**：每个问题都可以扩展成一次分享或复盘

如果你愿意，还可以把每个章节进一步扩展成：

- 自己的面试回答模板
- 公司内部 wiki
- 系统设计训练题集

## Contribution

欢迎通过 Issue 或 PR 一起继续完善：

- 修正文案和错别字
- 更新过时案例
- 增补现代实践
- 优化示例代码
- 提升章节可读性

## License

[CC-BY 4.0](LICENSE)
