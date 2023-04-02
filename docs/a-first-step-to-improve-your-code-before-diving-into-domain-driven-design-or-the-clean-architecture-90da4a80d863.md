# 在进入领域驱动设计或干净架构之前，改进代码的第一步

> 原文：<https://javascript.plainenglish.io/a-first-step-to-improve-your-code-before-diving-into-domain-driven-design-or-the-clean-architecture-90da4a80d863?source=collection_archive---------3----------------------->

## 软件设计

## 你可能听说过这两个概念:它们很聪明，但需要一些时间来实验和掌握。这里有一些技巧可以帮助你顺利缩小差距。

![](img/dfb850d24b0e449bd8b6c03a06376b0e.png)

既然你的代码库已经长大了，你是否觉得有问题，想回避新的开发？厌倦了花时间跟踪和修复臭虫，它甚至成了一场噩梦？因为你的软件没有负载而摧毁了你有前途的公司？

**你知道吗？我理解你的感受**……**我去年也经历过悲伤的时刻。**

在我的开发生涯中，我已经写了很多糟糕的、紧密耦合的、不可测试的、随机的代码，这些代码至今仍在生产中……我可能不是唯一一个这样的人，但是在思考了如何改进我自己和我的工作之后，我最终想到了一些可能解决这些问题的概念。

像*清洁代码(Martin Fowler)* 、*域驱动设计(Eric Evans)* 或者甚至*清洁架构(Robert C. Martin)* 这样具有大量相关模式的东西，比如 *CQRS* 、*聚合根*、*适配器、……*都是我们上面讨论的问题的流行解决方案。但这可能是个问题……

**🤔你为什么要读那篇文章？**

所有这些看起来(并且是)很酷，但是乍一看，对于新手和软件工艺新手来说，可能有点复杂。也许就像我的一些朋友一样，你还没有准备好开始这些方面的工作。

**慢慢来！慢下来:跳过步骤从来都不是一个好主意！**

因此，为了让过渡更顺利，我想与你分享一些原则和实践，当你决定对这些话题感兴趣时，这些原则和实践会对你有所帮助。

# 什么是软件开发中的好项目？

这是一个非常主观的问题，我将尝试将我的答案重新组合成我们在项目生命周期中可以观察到的四个核心原则/关键绩效指标:

*   让代码尽可能接近业务需求，以便适应它并增加“真正的”价值。(**真人**
*   能够完成应用程序的关键部分，以确保交付工作工具。一个好的项目只是在生产中运作，并在没有随机用户体验的情况下满足最初的需求。(**一致性**)
*   能够使应用程序具有可维护性、演进性和时间弹性。这不会在第一次开发人员变更或新框架更新时中断。这是一个易于掌握、部署和更新的应用程序。(**回弹力**)
*   有能力运送新的开发人员，新的开发或功能，或者只是在团队内切换开发人员，没有眼泪。(**适应性**

本文试图在学习那些架构原则和工作方式之前给你一些提示和想法，这样一旦你做好准备，理解 DDD、TDD、清洁架构原则和任何其他东西就更容易了。

# 软件开发中什么知识最重要？

![](img/9f020131b2cb7a114f1781e214679415.png)

你需要在那些与时间相关的事情上投入时间。我们看到了著名的 JS 疲劳期，它告诉我们总是有新的框架可以使用。**在此期间，你唯一可以依靠并且保持稳定的是你自己的业务规则，这些规则定义了你的项目 DNA。**

**我们可以利用那些使用编程基础的东西:干净的代码和软件架构。**

通过学习如何通过关注重要的东西来构建程序，以及如何用抽象来设计代码，你将能够使用任何框架或工具。这并不意味着你必须这样做，但你可以这样做。

环顾四周，所有的工作机会就像

*   高级反应开发者
*   VueJS 专家

我恭敬地认为这些提议是错误的。他们谈论实现细节，却忽略了最重要的方面:构建软件，这是一项与特定框架无关的技能。

理想情况下，您不需要 React 开发人员。你想要一个知道如何构建应用程序的开发人员，必须将业务逻辑连接到前端框架，在那里，为什么不使用 React。

# 在进入 DDD / Clean Architecture 之前，提高开发人员技能的一些原则。

## 1.在深入代码和数据模型化之前，在纸上思考用例以及核心领域事件

做申请的时候我们做什么？

我们利用计算机的处理能力解决现实生活中的问题。记住这一点。

制作一个不符合业务需求的应用程序毫无意义！花一些时间与业务团队一起定义上下文，并确保找到应用程序的核心事件和操作(领域)。

**这将帮助你围绕这些概念构建你的应用文件夹和代码。**

大多数开发人员(我以前是这方面的专家)正在考虑制作一个 UML 图或者查看我的实体将拥有哪些数据。这是一件坏事。

也不要考虑你的库、工具或框架如何适应你的业务需求，而是定义你的业务需求而不考虑框架的限制。然后，您将选择合适的工具来满足业务需求。

我们应该开始考虑动作(`bookACar`、`searchProducts`、…)，而不是先考虑实体(`Car`、`Products`)。通过这种方式，我们可以编写足够的代码来满足需求，因为变量字段会在我们需要时弹出。代码越少，潜在的错误就越少，程序的复杂性也就越低。

**此外，现在就开始在 IT 和业务之间使用一个通用的共享词汇表**

通常业务和开发团队不使用相同的措辞，这种引入绝对是灾难性的最终行为。花些时间正确地给业务命名，以确保你说的是同一件事。

> 投入生产的是开发团队已经理解的内容，而不是产品负责人或首席执行官的想法。

考虑上下文，想象一个电子商务应用程序:

*   ***产品是未来可能发生变化的东西***
*   ***而是开票上下文中的产品线*** (乍一看可能会被误认为是产品关系，但不应该！)是**被冻结**的东西，有独立的生命周期，就是它所来自的原始产品！

这种错误很常见，会给你的业务带来灾难性的影响。如果有人更新了一个项目的价格，而所有以前的发票都改变了价格，该怎么办？你错过了一些概念。

## 2.编写干净的代码

***干净代码有多种定义。***

对我来说:这是一个易于阅读的代码，被分成具有单一目的的指令，任何开发人员都可以使用它，而不会感到头痛，并对其行为充满信心。因为它很小，我们可以很容易地将代码指令与单元测试的其他代码模拟交换。

以下是一些制作干净代码的原则:

*   保持函数/类有一个**单一目的**，如果有一个以上的目的，只需将逻辑拆分到另一个函数/类中。
*   正确命名事物，当你阅读一个代码时，不应该产生歧义。使用像`List`这样后缀，用`customer`代替`user`这样的东西……试着用它们在商业术语中所代表的东西来命名。不要使用类似`a`或`b`的东西。
*   减少耦合，写没有副作用的纯函数。这样你就可以利用依赖注入和测试。

你可以在罗伯特·c·马丁的*干净代码手册*中读到更多

这就引出了第三个技巧:**减少耦合**

## 3.减少代码耦合考虑抽象

正如我们前面所说的，框架和工具只是业务逻辑的实现细节，不要过分依赖它们。例如，如果你需要一个支付工具，你可能会从 Stripe 开始，它非常受欢迎且易于使用。

如果你把你的代码和它紧密地结合在一起，当明天你不为这笔交易感到自豪，而费用条适用于你的时候，你会怎么把它换成另一个能让你少付钱的提供商呢？这肯定会非常困难，甚至可能会毁掉你的公司。

思考抽象有助于您将自己的业务逻辑从外部服务中分离出来。

您自己的业务逻辑可能是这样的:X 服务的提供商获得了多少报酬？或者，我的“现收现付”计划依靠什么来计算费用？。

首先要检查的是从大方法(称为*事务脚本*)中重构我们的代码，将它提取到以原语作为输入和输出(接口)的小函数/类中。

通过减少耦合和考虑抽象，我们可以轻松地编写代码，重用它，并通过提供一个假的实现来测试它。

同样:分两部分考虑应用程序:

*   你的应用程序的核心代码，你不能从任何其他地方得到，比如 sass 服务，数据库，用户输入。(**域代码**)
*   这个外部代码依赖于您使用的框架或外部服务(**基础设施代码**)

以这种方式思考，你就不依赖于实现，这就变成了一个细节。

## 考虑可重用性和领域驱动

不要按架构(事物是什么)打包你的代码，而是按域/模块(它们属于哪个域)打包。

很长一段时间，我使用像`Controllers`或`Reducers`这样的文件夹名打包，但是当项目长大后，它变得很难维护。

一个更好的方法是按领域打包，像`Users`或`Authentication`甚至`Payments`，在这些文件夹中，你保持代码小，并且在领域代码和实现代码之间分开。

*   按领域模块(与哪个领域相关)而不是基础设施(使用什么结构，像控制器、映射器:我们用来构建应用程序的工具)打包代码

这样做，如果做得正确，你甚至可以在项目和应用程序之间重用模块。即使看起来不那么远，您也可以更容易地在模块之间共享代码，因为它们耦合度更低

**这是一个简单的介绍**

我希望所有这些能够帮助你在软件架构的世界里迈出第一步。一旦你想尝试 DDD 或清洁建筑，通过应用这四个概念，你会帮助你自己。

## [↓ For French People↓↓我建议您浏览 Coding Spark 并订阅我的时事通讯,免费获取科技内容!(T1 )](https://codingspark.io/?referral=medium)