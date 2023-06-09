# 条纹面试问题:最小缺失正整数

> 原文：<https://javascript.plainenglish.io/stripe-interview-question-lowest-missing-positive-integer-f40d9dd0272b?source=collection_archive---------5----------------------->

## 如果你去 Stripe 面试，要做好准备

![](img/34f1b5ea4f4366ba518e50a4d3f1e188.png)

Taken from [stripe.com](https://stripe.com)

可怕的白板编码面试。我们都讨厌它，但我们都必须面对它。

这已经成为公司测试候选人编程能力的标准——尤其是对于初级到中级职位。所以，让我们提高技能，今天就尝试一个。

在几个不同的国家呆过一段时间后，我在伦敦、新德里、旧金山、芝加哥、新加坡、柏林和慕尼黑建立了一个强大的软件相关职位的朋友网络。

在这种情况下，我分享一些在我的网络中分享的东西——一个在谷歌采访中被问到的问题。

# 问题

给定一个整数数组— `numbers`，从该数组中找出最小的可能丢失的正整数。正整数是大于 0 的任何整数。下面是一些帮助你理解的例子。示例 1:

输入 1: `[0, 1, -2, 2, 4]`

产出 1: `3`

下面是例子 2:

输入 2: `[1, 2, 3, 4]`

产出 2: `5`

下面是例子 3:

输入 3: `[2, 3, 4]`

输出 3: `1`

# 解决办法

在这里找到一个低效的解决方案非常容易——您可以过滤数组以删除所有负数，然后对其进行排序，然后遍历数组以找到两个元素之间的任何间隙。然而，由于最快的排序算法具有`O(n log n)`时间复杂度，因此寻找具有`O(n)`时间复杂度的解决方案还有一些改进的空间。

> “如果我们考虑这个问题，我们必须认识到，我们能得到的最低可能答案将在 1 和输入数组长度+ 1 的范围内。”

因为 1 是最小的正整数，它总是我们的范围的下限，假设在最坏的情况下，如果数组包含所有正数，下一个可能的正整数将是 1 +输入数组的长度。如果我们看例子 2，这是不言而喻的；由于所有正整数都达到了数组的长度，所以最小的整数等于输入数组的长度(5)。让我们将这个解决方案付诸实践:

在上面的解决方案中，我们创建了一个新的数组，并对它进行了初始化，使其包含一个零，稍后你会明白为什么。当我们遍历输入数组`numbers`时，如果一个整数是正的，我们就把它添加到我们的效用数组`positiveIntegers`中该整数的值的索引处。因为我们的数组已经有了`0`，而且因为我们只在数组中添加正数，并且这些数字已经存在于`numbers`数组中，所以有两种情况:

1.  或者，在我们的`positiveIntegers`数组中有一些空隙，也就是说，在 JavaScript 世界中，数组中的一些元素在我们的`undefined`中，所以我们将找到我们最不可能丢失的正整数
2.  或者，我们的数组中没有间隔，因此，如果我们到达数组的末尾，我们可以从逻辑上得出结论，丢失的最小可能正整数是下一个整数，因此，我们将返回数组的长度，它可以等于`numbers.length + 1`或`numbers.length`，这取决于`numbers`是否包含任何负整数或`zero`。

这个解决方案是可行的，并且具有 O(n)时间复杂度。但是，我希望您想一想，如果我们收到此输入，会发生什么情况:

`[1, 1000000]`

我们的函数将正常工作，并给出一个`2`的输出，但是您能想象在这个解决方案中，我们必须创建的数组的大小吗？

`[0, 1, undefined, undefined, undefined, undefined, ..., 1000000]`

所以即使我们的时间复杂度会是`O(n)`我们的空间复杂度会有问题，我也不知道怎么用大 O 记号表示:`O(x)`？

# 改进的解决方案

现在让我们尝试一个解决方案，我们使用类似的技术，所以我们保持相同的时间复杂度，但是我们将使用 HashSet，而不是创建一个新的(可能)非常大的数组，这在 JavaScript 中被简单地描述为一个 [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) ，但是也可以用一个简单的基本 JavaScript 对象来完成。但是使用内置的 Set 对象，使得编写代码更容易，所以让我们使用它。JavaScript 中的集合是一个 JavaScript 对象，允许您存储唯一值并遍历它们。这就是现在的解决方案:

这里，我们只是从最小的正整数(1)开始遍历集合，然后再往上一步，直到找到一个不包含在集合中的整数。这个改进的解决方案的伟大之处在于，我们使用的空间复杂度仍然与输入数组的大小成正比`numbers`，因此我们的时间和空间复杂度都是`O(n)`。

# 不同的 JavaScript 引擎呢？

我知道 Google 的 V8 JavaScript 引擎使用散列表实现了`Set`和其他一些数据结构，比如`Map`。本文详细介绍了它们的实现。然而，由于 [ECMAScript 2015 文档](http://www.ecma-international.org/ecma-262/6.0/index.html#sec-set-objects)指出:

> Set 对象必须使用哈希表或其他机制来实现，平均来说，这些机制提供的访问时间与集合中的元素数量呈次线性关系。

因此，这意味着如果你正在为 Node.js 或 Google Chrome/Chromium 浏览器或任何其他使用 Google V8 引擎的浏览器编程，你的代码将以 O(n)时间复杂度运行，因为检索一组对象的值，即我们使用的`set.has(x)`方法将只有一个`O(1)` /常数时间。但是如果你正在为一个旧的浏览器编程，你可能不得不重新考虑你的解决方案，并且很可能这个旧的浏览器甚至不支持一个仅随 ES6 而来的`Set`实现。尽管如此，在编程面试中，如果你表现出对 HashSet 数据结构的理解，面试官不会关心语言的具体实现。

实际上，您可以重构这段代码来处理一个简单的 JavaScript 对象，而完全不使用`Set`实现。这应该很容易，尤其是如果你理解我们在最终解决方案中所做的逻辑。或者更好的是，你可以使用更传统的语言，比如 Java，其中只有一个数据结构的实现，比如 HashTable 和 HashSet。

如果我错过了什么，请在下面发表评论！如果你喜欢这样的内容，请在这里关注我，因为我有更多这样的问题，我打算张贴出来帮助你磨练你的白板编码面试技巧！

## **用简单的英语写的 JavaScript 的注释:**

我们总是有兴趣帮助推广高质量的内容。如果你有一篇文章想用简单的英语提交给 JavaScript，用你的 Medium 用户名给我们发邮件到[submissions@javascriptinplainenglish.com](mailto:submissions@javascriptinplainenglish.com)，我们会把你添加为作者。

我们已经推出了三种新的出版物！请关注我们的新出版物:[**AI in Plain English**](https://medium.com/ai-in-plain-english)[**UX in Plain English**](https://medium.com/ux-in-plain-english)[**Python in Plain English**](https://medium.com/python-in-plain-english)**——谢谢，继续学习！**