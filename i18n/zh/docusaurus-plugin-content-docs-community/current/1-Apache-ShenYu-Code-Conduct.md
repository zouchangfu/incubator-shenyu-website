---
title: 编码指南
description: Apache ShenYu 编码指南
author: "xiaoyu"
categories: "Apache ShenYu"
tags: ["Code Conduct"]
date: 2019-04-09
cover: "/img/architecture/shenyu-framework.png"
---

## 开发理念

- **用心** 保持责任心和敬畏心，以工匠精神持续雕琢。
- **可读** 代码无歧义，通过阅读而非调试手段浮现代码意图。
- **整洁** 认同《重构》和《代码整洁之道》的理念，追求整洁优雅代码。
- **一致** 代码风格、命名以及使用方式保持完全一致。
- **精简** 极简代码，以最少的代码表达最正确的意思。高度复用，无重复代码和配置。及时删除无用代码。
- **抽象** 层次划分清晰，概念提炼合理。保持方法、类、包以及模块处于同一抽象层级。

## 代码提交行为规范

- 确保通过全部测试用例，确保执行`./mvnw clean install`可以编译和测试通过。
- 确保覆盖率不低于master分支。
- 确保使用Checkstyle检查代码，违反验证规则的需要有特殊理由。模板位置在`https://github.com/apache/incubator-shenyu/blob/master/script/shenyu_checkstyle.xml`，请使用checkstyle 8.8运行规则。
- 应尽量将设计精细化拆分；做到小幅度修改，多次数提交，但应保证提交的完整性。
- 确保遵守编码规范。

## 编码规范

- 使用linux换行符。
- 缩进（包含空行）和上一行保持一致。
- 类声明后与下面的变量或方法之间需要空一行。
- 不应有无意义的空行。请提炼私有方法，代替方法体过长或代码段逻辑闭环而采用的空行间隔。
- 类、方法和变量的命名要做到顾名思义，避免使用缩写。
- 返回值变量使用`result`命名；循环中使用`each`命名循环变量；map中使用`entry`代替`each`。
- 配置文件使用`Spinal Case`命名（一种使用`-`分割单词的特殊`Snake Case`）。
- 需要注释解释的代码尽量提成小方法，用方法名称解释。
- `equals`和`==`条件表达式中，常量在左，变量在右；大于小于等条件表达式中，变量在左，常量在右。
- 除了构造器入参与全局变量名称相同的赋值语句外，避免使用`this`修饰符。
- 除了用于继承的抽象类之外，尽量将类设计为`final`。
- 嵌套循环尽量提成方法。
- 成员变量定义顺序以及参数传递顺序在各个类和方法中保持一致。
- 优先使用卫语句。
- 类和方法的访问权限控制为最小。
- 方法所用到的私有方法应紧跟该方法，如果有多个私有方法，书写私有方法应与私有方法在原方法的出现顺序相同。
- 方法入参和返回值不允许为`null`。
- 优先使用三目运算符代替if else的返回和赋值语句。
- 优先考虑使用`LinkedList`，只有在需要通过下标获取集合中元素值时再使用`ArrayList`。
- `ArrayList`，`HashMap`等可能产生扩容的集合类型必须指定集合初始大小，避免扩容。
- 日志与注释一律使用英文。
- 注释只能包含javadoc，todo和fixme。
- 公开的类和方法必须有javadoc，其他类和方法以及覆盖自父类的方法无需javadoc。

## 单元测试规范

- 测试代码和生产代码需遵守相同代码规范。
- 单元测试需遵循AIR（Automatic, Independent, Repeatable）设计理念。
  - 自动化（Automatic）：单元测试应全自动执行，而非交互式。禁止人工检查输出结果，不允许使用`System.out`，`log`等，必须使用断言进行验证。
  - 独立性（Independent）：禁止单元测试用例间的互相调用，禁止依赖执行的先后次序。每个单元测试均可独立运行。
  - 可重复执行（Repeatable）：单元测试不能受到外界环境的影响，可以重复执行。
- 单元测试需遵循BCDE（Border, Correct, Design, Error）设计原则。
  - 边界值测试（Border）：通过循环边界、特殊数值、数据顺序等边界的输入，得到预期结果。
  - 正确性测试（Correct）：通过正确的输入，得到预期结果。
  - 合理性设计（Design）：与生产代码设计相结合，设计高质量的单元测试。
  - 容错性测试（Error）：通过非法数据、异常流程等错误的输入，得到预期结果。
- 如无特殊理由，测试需全覆盖。
- 每个测试用例需精确断言。
- 准备环境的代码和测试代码分离。
- 只有junit `Assert`，hamcrest `CoreMatchers`，Mockito相关可以使用static import。
- 单数据断言，应使用`assertTrue`，`assertFalse`，`assertNull`和`assertNotNull`。
- 多数据断言，应使用`assertThat`。
- 精确断言，尽量不使用`not`，`containsString`断言。
- 测试用例的真实值应名为为actualXXX，期望值应命名为expectedXXX。
- 测试类和`@Test`标注的方法无需javadoc。

**以上内容参考了[Apache ShardingSphere的编码指南](https://shardingsphere.apache.org/community/cn/contribute/code-conduct/)，并做了适当调整。**
