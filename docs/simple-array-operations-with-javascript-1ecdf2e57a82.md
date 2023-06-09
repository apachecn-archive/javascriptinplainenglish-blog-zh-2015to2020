# 用 JavaScript 进行简单的数组操作

> 原文：<https://javascript.plainenglish.io/simple-array-operations-with-javascript-1ecdf2e57a82?source=collection_archive---------17----------------------->

## 通过使用本机数组辅助函数简化 JavaScript 中的集合操作

![](img/5461567ff29bc60cf4f855e580962495.png)

Made by the author in [Canva](https://www.canva.com/)

JavaScript 提供了许多数组助手函数，可以处理数组操作的大部分繁重工作。在本文中，我将通过几个这样的操作的例子来演示它们是如何帮助简化代码编写的。

我将在本文中讨论的函数包括`.map()`、`.filter()`、`.reduce()`、`.some()`和`.find()`。我使用这些强大的函数已经有好几年了，我甚至都不记得我最后一次写标准的`for`循环来处理数组是什么时候了。一旦你掌握了如何使用它们，你就不会回头了。

对于其中的每一个，我都将使用示例来演示与更传统的方法相比，这如何简化代码。让我们开始吧！

# 。map()和。过滤器()

我们先通过实例介绍`.map() and` `.filter()`。当我开始用 Redux 开发我的第一个 React 应用程序时，我真正开始大量使用它们。

如果你熟悉 Redux，你会意识到它背后的思想是存储在 Redux 中的数据是不可变的。换句话说，您总是在创建新的数组或对象，而不是改变现有的数据。这种创建新引用而不是改变现有引用的想法是不变性的关键。

这些数组函数很方便，因为在`.map()`和`.filter()`的情况下，它们总是返回对新数组的引用。这使得检测应用程序中的变化变得简单。

例如，如果您有一个数组引用作为 React 应用程序中某个挂钩的依赖项，那么很容易检测到何时重新运行该挂钩，因为您只在数组引用更改为新数组时激活它，而不是尝试检测添加、删除等。

在我们开始看例子之前，我们将创建一个包含少量对象的数组，这样我们就有一个集合可以处理了。

让我们从执行一个简单的操作开始。比方说，我们希望将所有的 id 放入一个数组中。这是使用`for`循环时的样子。

我们创建一个数组，然后循环遍历这些值，并将所有的 id 放入该数组，以获得 id 列表。我们可以通过使用`.map()`来简化这个操作

这给了我们和以前一样的结果，但是我们不需要创建一个变量然后赋值，我们可以在一个步骤中完成。我们可以进一步简化。我们可以在我们写的箭头函数中使用隐式返回。

*即与* `*.map()*` *基本概念相同。它用于创建一个数组，原始集合中的每一项都有一个结果。*

对于我们的下一个例子，我们将使用与`.map()` 不同的`.filter()`，它将返回一个新的数组，但是它不会为原始集合中的每一项都有一个条目，除非该数组中的所有项都满足`.filter()`的条件。

假设我们想要得到一个已经登录并且登录超过 50 次的所有人的列表。首先，我们将通过一个`for`循环来实现。

和我们之前做的非常相似。我们创建一个新数组来保存结果，然后遍历集合，将满足条件的结果添加到新数组中。

就像之前一样，让我们展示如何使用`.filter()`将这两个步骤合并成一个步骤

结合使用`.filter()`和`.map()`可以使它们更加有用。因为每个操作的返回都是一个新的数组，所以如果需要一次应用多个操作，将它们链接在一起非常简单。

例如，我们可以将第一个示例与第二个示例结合起来，获得每个处于活动状态且登录次数超过 50 次的用户的 id。

您可以看到这是多么有用，因为在将每个对象映射到 id 之前，我们将列表过滤为我们感兴趣的对象。

# 。减少()

我记得几年前的一次面试，面试官让我解释如何使用`.reduce()`。当时，我毫无头绪，但面试官热情地告诉了我。我引用他的原话“reduce 是所有阵列操作中的老大”。现在我很熟悉了，我完全同意这种观点。

与。reduce()你可以把一个集合转换成一个单独的对象。比方说，我们想要为每个用户 id 创建一个带有键的对象，这样我们就可以使用它轻松地查找用户。

让我们看一个例子。

在上面的例子中`acc`是累加器对象。我们用`{}`初始化累加器，所以一开始它只是一个空对象。在每次迭代中，通过集合，我们使用扩展操作符(`…acc`)来“扩展”累加器中已经存在的所有键/值，然后添加当前 id 作为键，添加当前用户对象作为值。

# 。一些()和。查找()

我们要复习的最后几个例子包括`.some()`和`.find()`。如果我需要在一个数组中寻找一个值，我发现自己经常会同时使用这两种操作。

我们可以使用`.some()`来找出数组中的任何对象是否满足我们的条件。假设我们想看看列表中是否有活跃用户。

这将返回一个布尔值，表明是否至少有一个对象符合我们的标准。`.find()`很相似。唯一不同的是。find()将找到满足我们条件的第一个对象，然后返回该对象。

*我一直在寻找编写 JavaScript 的更好方法，所以如果你不熟悉本文中的数组操作，我希望这有助于澄清你的理解。感谢阅读！*

喜欢这篇文章吗？如果有，通过 [**订阅获取更多类似内容解码，我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw) **！**