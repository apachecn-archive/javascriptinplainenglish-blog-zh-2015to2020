# 如何为一个众所周知的问题找到一个体面的解决方案

> 原文：<https://javascript.plainenglish.io/how-to-find-a-decent-solution-to-a-well-known-problem-cbb9e7e6d44e?source=collection_archive---------3----------------------->

![](img/0aaa9604b31a3329c401f100cca367c0.png)

Photo by [Maarten Deckers](https://unsplash.com/@maartendeckers?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我最近发现了两篇相互关联的文章:

*   [https://medium . com/free-code-camp/bet-you-cant-solve-this-Google-interview-question-4 a 6 e 5 a 4d c8 ee](https://medium.com/free-code-camp/bet-you-cant-solve-this-google-interview-question-4a6e5a4dc8ee)
*   [https://medium . com/@ bosqueviejo/I-bet-my-elixir-solution-is-bet-than-yours-in-JavaScript-62a 3860 b4b 3c](https://medium.com/@bosqueviejo/i-bet-my-elixir-solution-is-better-than-yours-in-javascript-62a3860b4b3c)

两位作者都声称对一个众所周知的问题有很好的解决方案——一个用 JavaScript 编写，另一个用 Elixir 编写。

当我读这两篇文章时，我立刻对他们处理这个问题的方式感到不舒服。两者都只考虑了技术方面而没有更深入地看它的核心问题。这是阻碍简单解决方案的主要原因。

# 我的最佳实践

为了找到一个体面的解决问题的办法，我总是努力遵循这些规则:

*   用自己的话表达问题，尽可能多地抓住问题的方方面面
*   用简单的语言写下解决方案
*   将解决方案隔离在逻辑块中
*   想想边缘案例
*   选择正确的工具来实施
*   按照你写好的解决方案去实现它

*那我们就这么做吧！*

## 表达问题

假设您有一个包含不同颜色节点的行和列的网格。行数、列数和颜色将在运行时定义。你现在的任务是找到由具有共同边界的每个邻居的相同颜色链接的节点的最大区域。

如果你现在能想象出来，那你就答对了！

## 写出解决方案

当然，网格可以用二维数组来表示。但是是什么阻止我们使用一维数组来保存行号和列号作为属性呢？
考虑到网格，每个节点有 2 到 4 个可能的邻居来检查相同的颜色，并最终建立一个区域。我们必须检查所有 4 个邻居吗？显然不会，因为每一个北部和西部的邻居都会再次受到其南部和东部邻居的检查。好的，这意味着如果我们只看北部和西部的邻居，我们可以在一个周期内遍历网格，只需要处理已经创建的节点。
那我们如何建设这片区域呢？让我们向节点添加另一个属性:area。对于每一个找到的具有相同颜色的邻居，我们将节点的索引添加到这个区域，建立一个节点链(作为一个数组)。
现在事情变得有点复杂了。添加到邻居区域的节点可能已经建立了自己的链。因此，我们必须将节点区域的所有成员添加到邻居区域中。
最后但并非最不重要的，我们需要维护一个对邻居区域的引用，其中节点的区域已经被添加。这样，我们总是知道节点属于哪个区域。

这是最难的部分。但是如果做对了，你会有一个简单的指南可以遵循。

## 隔离

*   循环遍历长度为行 x 列的数组:
*   向该数组添加一个具有以下属性的节点:color(随机生成)、area(存储成员)和 ref(存储该节点所属区域的引用)
*   按顺序检查西边和北边的邻居(如果有的话):如果节点和邻居共享相同的颜色但不共享相同的区域(通过检查引用)，循环遍历节点的区域，将每个成员放入邻居的区域，并将节点成员的引用调整为邻居的引用。
*   通过比较每个节点的 area 属性的长度找到最大的面积。

*这已经为使用伪结构实现扫清了道路。*

## 边缘案例

我看到两个边缘案例:

*   如果只有一种颜色会怎么样？
    将所有节点添加到第一个节点的区域。所需的资源与其他情况没有什么不同。
*   网格大小的极限在哪里？
    随着网格大小的增加，所需资源呈线性增长[O(n)]，唯一的限制是相应语言的 eco 系统中授予数组的内存。

*在这里，我们没有发现在设计的解决方案中需要实施的任何限制。*

## 选择正确的工具

事实证明，我们没有实现高度复杂的算法。因此，任何以适当方式处理数组的语言都应该足够了。

*我再次选择 JavaScript，因为我很好奇这个算法能不能打败 Elixir 的。*

## 实施

开始了。

我相信你能够按照上面的描述解决问题。它有 26 行代码，在一个周期内创建网格的同时构建区域。

# 表演

为了测量性能，我使用了以下代码:

下面是使用 100x100 的三色网格进行的比较

*   第一个 JavaScript 解决方案大约需要 230 毫秒
*   酏剂的解决方案需要大约 90 毫秒
*   我们的解决方案平均需要 13 毫秒

# 结论

实现的技术方面不应该驱动解决方案。如此例所示，一个好的解决方案基础可以通过多种因素击败一个差的。

我希望你喜欢阅读，有一个伟大的时间！