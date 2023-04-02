# 代价高昂的错误:为什么我们不得不放弃 Firebase

> 原文：<https://javascript.plainenglish.io/costly-mistakes-why-we-had-to-abandoned-firebase-b89930c10d92?source=collection_archive---------0----------------------->

## 随之而来的是三年的工作。

![](img/b860324a62ad41133488950f06b3a695.png)

Photo by [Nick Jio](https://unsplash.com/@nicholasjio?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/abandon?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

那一年是 2018 年。我们快要毕业了。我们有一个伟大的想法，我们认为这将使我们成为亿万富翁(剧透:它没有)。

但是有一次一个伟大的头脑说一个伟大的想法本身不算数。你需要执行力。

所以需要建造这该死的东西。我们必须尽快完成。但我们是一个只有 4 名成员的团队。

所以我们都开始做研究(主要是谷歌搜索👊)找出最快、最简单的方法来生产我们可以在一夜之间运送给数百万客户的产品。

答案是**火焰基地。我们被许诺了伟大的事情。这对我们来说是完美的解决方案。**

## 促使我们选择 Firebase 的原因

*   不需要后端工程师。我们只需要建立前端。
*   免费层相当慷慨。
*   基本没有准入门槛。
*   非常好用。
*   几乎拥有我们需要的一切。
*   最重要的是，它是由谷歌建造的。

Firebase 确实有一些很棒的特性。非常适合初学者。我们经常使用的一些功能有

*   **Firestore:** 这是一个高度可扩展的实时 NoSQL 数据库解决方案，可以由任何前端直接使用。
*   **认证:**我们根本不用担心系统的认证部分。Firebase 完全掩护了我们。
*   存储:我们使用 Firebase 存储主要存储我们的图像。
*   **通知:** Firebase 提供了一个非常容易实现的通知服务。
*   托管: Firebase 让我们托管静态网站变得超级简单。我们的前端 React 应用程序是使用 Firebase 托管的。
*   **功能:**它们运行在云上。它们可以对您的数据级别上的任何类型的事件做出响应。我们主要使用这个服务来发送通知。

所以我们在所有的项目中都使用了 Firebase。从移动应用程序到 web 面板。我们确实在很短的时间内取得了良好的进展，甚至为我们自己管理了资金。

在我们不得不扩大规模之前，一切都很顺利。我们有一些新的团队成员来帮助我们完成项目。我们的仪表板和管理面板需要更多的定制。事情开始出错。

让我解释一下。。。

## 不一致的数据

由于 Firebase Firestore 本质上是 NoSQL，因此可以推送的数据没有限制。

因此，可能一些开发人员添加了一些额外的字段或忘记对值进行空检查，整个应用程序崩溃了。

每次我们把一些东西推向生产，我们必须祈祷它不会破坏其他东西。

随着越来越多的开发商开始加入，问题也越来越多。每个错误都浪费了我们很多时间。不值得。核心成员不得不夜以继日地工作，仅仅是为了让产品存活下去。

每一部新电影都是一场噩梦。

## 一致性

Firebase 在字段级别为**事务**提供了一些机制。但是很难维持。

有人可能会存储一个名为**用户标识**的字段，如果其他人通过字段**用户标识**推送另一个用户，整个应用程序就会崩溃

因为我们不得不直接从前端操作数据库，许多不好的事情发生在前端。也许用户关闭了他的应用程序或者设备关闭了。很难找到任何问题的确切原因。

![](img/a1c106ab171fd55e446721177355cb30.png)

Photo by [Matias Malka](https://unsplash.com/@matiasmalka?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/frustration?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## 加入多个集合

您无法连接两个集合来获取一些数据。

例如，您有一个**用户**集合。您还有另一个用于**车辆**的集合，您需要用它来存储车主的信息。因此，您必须在车辆集合中保留用户的 id。

现在想象一个场景，您需要显示带有车主姓名的车辆列表。

Firebase 的解决方案是

1.  加载车辆列表。
2.  从它们中获取用户 id。
3.  分别给每个用户打电话以获取他们的详细信息。

现在想象一下，如果你必须用它来显示其他数据。可能需要存储车辆驾驶员信息。

你能明白我的意思吗？

## 数据复制

为了避免与连接集合相关的问题，我们通常不得不采取的解决方案是在集合之间复制数据。所以现在如果我们要在创建的时候创建一辆车，我们必须存储关于它的所有者的数据。

因此，当我们需要显示数据时，我们只需获得车辆的数据，而不必担心车主并进行第二次呼叫。

但是这个解决方案也带来了一些其他的问题。现在，无论何时任何用户更新他的信息，我们都必须随时更新数据。所以我们必须跟踪存储用户信息的所有集合。

找到最佳点非常困难。

## 代码复杂性

因此，随着我们的查询变得复杂，前端代码也变得复杂。此外，我们必须对所有内容进行两次编码。一次用于移动设备，另一次用于 web 前端。

为了更新产品系列，我们不能再依赖单个团队成员了。

我们采用了 Firebase 本身提供的解决方案，即 Firebase 函数。

基本上，一些数据更改可以触发 Firebase 函数。这些函数是使用 typescript 编写的，托管在 Firebase 上。

因此，作为一个解决方案，每当任何用户更新他们的信息时，我们必须触发一个函数来更新该用户的所有相关字段。

现在最初问题的解决方案变成了问题本身。基本上，现在我们所做的是从 3 个地方访问和更新数据。

## 效率

随着我们的团队越来越大，我们再也无法应付了。我们不得不投入大量的时间和资源来维护数据的完整性，但仍然无法高效地查询我们的数据。

每个开发人员现在都必须非常小心地做每一件事，以免弄坏东西。强制每个人遵循一些通用规则和命名约定需要一些时间。

## 费用

Firebase 确实为其所有服务提供了一个免费层。但是在那之后，它变得非常昂贵。之后，成本取决于文档读取的次数。

由于我们必须在各种集合之间保持高度的一致性，账单堆积如山。已经不值得了。

## 启示

所以在面对所有这些问题之后，我们最终决定继续前进。

我们决定使用 Node.js 和 Postgres 重写我们的整个后端。对于主机，我们现在使用 AWS。

我们仍然使用 Firebase 进行身份验证和通知。

## 那么 Firebase 对每个人都不好吗？

最简单的答案是否定的。仍然有很多你应该考虑使用 Firebase 的用例。

*   首先，这是一项很值得学习的技术。如果你开始你的职业生涯，你应该学习它。这有助于很容易地熟悉数据存储技术。
*   对于通知和用户认证，它仍然是一个很好的简单的解决方案。
*   如果你是一个独立开发者或自由职业者，你需要快速行动，你应该使用 Firebase。
*   如果你正在做的项目规模很小或供内部使用，你应该考虑它。

但是

*   如果你想做点正经事。
*   如果你想让你的项目被很多人使用。
*   如果您的项目需要一些复杂的数据操作。
*   如果你想学一些对你长远有帮助的东西。

那么去 Firebase(至少对我们来说)是一个大禁忌。你应该去看看别的东西。

今天到此为止。编码快乐！

**通过** [**LinkedIn**](https://www.linkedin.com/in/56faisal/) **或我的** [**个人网站**](https://www.mohammadfaisal.dev/) **与我取得联系。**