# 你需要编写有效的单元测试

> 原文：<https://javascript.plainenglish.io/you-need-to-write-effective-unit-tests-954f60319f0a?source=collection_archive---------9----------------------->

![](img/6b63f5693bc2936ca0ea67dfb768e8d3.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

编写单元测试已经成为软件工程师的日常任务。编写单元测试有几个目的:

*   **更好的产品体验&品质**。公司希望推出问题较少的产品。
*   **省时**。确保开发的增强工作如期进行，减少**叮咚游戏**这样我们就可以减少修复 bug 的时间，即运行时间。例如，用于 QA->Dev->QA->Dev->QA->部署。
*   **提高工程师的信心**。如果你编写单元测试，你可能会在开发和发布的过程中获得更多的信心。

既然单元测试带来了这么多好处，但是为什么会有出错的可能性。例如，

> 经理:你好，德隆，你昨天工作的票有些问题。你能看一下吗？
> 
> 我:当然。会调查的。
> 
> 我(自言自语) :昨天所有的单元测试都通过了。为什么仍有问题提出？

这种情况你听起来熟悉吗？它确实在我身上发生了很多次。

因此，我决定找出我可以做得更好，以减少这种情况，提高我的生产力。

# 编写有效的测试

结果是我写的单元测试根本没有效果。准确地说，我写的单元测试不够具体。下面我们来看一些例子。

假设我们有一个名为`clientController`的文件。有一个`getClient`函数，我们可以在其中检索客户信息。

## 我为控制器编写的普通简单测试用例

下面是我将编写的测试`getClient`功能的简单测试用例。

以上测试用例通过。然而，这个测试用例并不**有效**，因为它不够**具体**。我刚刚验证了

*   我们验证要调用的`res.json`。但是我从来不知道它返回了什么。是否返回了正确的客户信息？

因此，这里有什么需要特别说明的呢？

*   期望**返回的客户信息正确**。

一个更具体的单元测试应该是这样的。

## 更好的单元测试(更具体)

多了两行代码。现在单元测试被处理得更具体了，它是一个有效的单元测试。

# 结论

以下是这篇文章的要点。

*   编写单元测试是不够的，您需要编写有效的单元测试。
*   有效的单元测试总是由特异性贡献的。这意味着您期望的结果越具体，您的单元测试就越有效和准确。

感谢您的阅读。下一篇文章再见。

*原创文章发表在我的* [*博客*](https://tekloon.dev/writing-effective-unit-test) *上。*