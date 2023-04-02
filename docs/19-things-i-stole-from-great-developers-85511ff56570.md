# 我从伟大的开发者那里偷来的 19 样东西

> 原文：<https://javascript.plainenglish.io/19-things-i-stole-from-great-developers-85511ff56570?source=collection_archive---------0----------------------->

## 伟大的开发人员每天都在做什么

![](img/c1dc6a551366f7b806b5f178cb6d4aef.png)

Photo by [Thirteen .J](https://unsplash.com/@thirteeeeeeen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 三法则。

是代码重构的经验法则，用来决定何时应该用新的代码/过程/方法替换一段复制的代码。

> 它声明允许您复制和粘贴代码一次，但是当相同的代码被复制三次时，它应该被提取到一个新的过程中。

主要概念是使代码/过程/方法通用化，这样它可以在许多地方重用。

## 一致性是王道

与结构和编码方式保持一致。这有助于提高应用程序的可读性和可维护性。

尝试提出有助于一致性的编码标准。它应该和变量的命名约定一样少。另一个大问题是应用程序的结构，开发者需要做出改变或添加新东西的地方应该很明显。

## 减少嵌套

`if`中的`if`会变得混乱，很难读懂，非常快。有时你可能无法绕过这一点，但总是看看你的代码结构。

对于`else if`来说也是如此。尽可能避免，因为这有时会使代码更难阅读。

一个**保护条款**是帮助解决这个问题的有效方法！

> guard 子句只是一个立即退出函数的检查，要么带有 return 语句，要么带有异常。

***不带*** *一个守护子句:*

```
if (account != null)
{
    if (order != null)
    {
        if (order.term == Term.Annually)
        {
            // term annually
        }
        else if (order.term == Term.Monthly)
        {
            // term monthly
        }
        else
        {
            throw new InvalidEnumArgumentException(nameof(term));
        }
    }
    else
    {
        throw new ArgumentNullException(nameof(subscription));
    }
}
```

***同*** *一个守护子句:*

```
if (account == null)
{
        throw new ArgumentNullException(nameof(account));
}if (order == null)
{
    throw new ArgumentNullException(nameof(order));
}if (order.term == Term.Annually)
{
    // term annually (return here)
}if (order.term == Term.Monthly)
{
    // term monthly (return here)
}throw new InvalidEnumArgumentException(nameof(order.term));
```

## 想想更大的图景

理解大局是非常重要的，这样才能让小细节更容易理解。一旦你理解了大局，小细节不会让你花太多时间去理解。

## 花时间思考命名事物

在编码中命名是你能做的最难的事情之一。这可以是命名一个类、方法，甚至是一个变量。

优秀的开发人员会花时间考虑相关的名字，因为他们知道这有助于可读性！

## 技术债务是不好的

高估可以帮助解决这个问题。尽你所能地写一遍，否则你将不得不一遍又一遍地重复。

> **技术债务**是软件开发中的一个概念，它反映了由于现在选择一个简单的(有限的)解决方案而不是使用一个需要更长时间的更好的方法所导致的额外返工的隐含成本

## 估计过高

这可能是一个奇怪的问题，取决于你在哪个部门工作，你可能不喜欢这一点，但你会看到伟大的开发人员高估任务，因为他们知道事情总是需要比你预期的更长的时间，增加一个缓冲估计可以真正帮助你把事情做好。

这个真的可以帮到上面那点*“技术债不好”。*如果你低估或估计一个只考虑快乐路径的时间，这实际上会产生技术债务，因为你只有时间让它工作，而不是让代码干净和易于维护。

## **文档和代码注释**

它们有助于保存背景和分享知识。你会听到更有经验的人不断地说，我们能记录那个过程吗，或者不能通过代码审查，因为没有关于接口之类的东西的评论。

## 对删除不良代码有信心

你会看到很多不太自信的开发人员注释掉大量代码，然后把它们留在那里。版本控制是有目的的！优秀的开发人员不会回避删除应用程序中不好的部分。

## 花时间在代码评审上

优秀的开发人员会在代码评审上花费更长的时间，并且知道代码评审的重要性。

*   帮助尽早发现 bug
*   提高开发人员的技能，并让团队的其他成员采用良好的实践。
*   分享知识
*   一致的设计和实施

我见过的最好的代码审查过程是:

*   **一个风险很小的小任务**应该由一个开发人员在他们的办公桌前评审。
*   中型/大型变更或有风险的变更应该由 3 名开发人员审核，其中一名是他们办公桌前的高级开发人员。
*   **一个极其危险的变化或正在开发的应用程序的一个新部分**应该预约一个会议，3 个开发人员至少其中一个是首席开发人员一起检查每一行并提出要点。

## 编写好的测试

你会注意到更有经验和更强的开发人员会花更多的时间来编写好的测试。

拥有好的测试有助于你更有信心地扩展你的应用程序，并有助于减少产品缺陷。

## 花时间设计

在深入研究代码之前，他们会仔细思考并将其分解成小块。这有助于他们更好地准备所有的东西如何组合在一起，并创建更清晰的代码。

## 关注基本原理，而不是语法

这是一个大的！他们喜欢学习基础知识，而过于关注语法。这有助于他们更有效地发现问题。这也可以帮助他们对谷歌问题有更多的了解。

## 让谷歌成为你最好的朋友

他们是用谷歌搜索帮助他们解决问题的专家。这种帮助是因为上面提到的*“关注基础而不是语法”。*

因为他们专注于基本面，他们知道谷歌搜索什么。如果你痴迷于学习语法，这是很难做到的！

## 先确保它能工作，然后再让它变得漂亮

你会在较弱的开发人员身上看到这种情况，他们似乎花了太多时间在开始时让它看起来很漂亮，然后发现他们的代码行不通。

伟大的开发人员在早期工作时会有一条快乐的道路。帮助他们在事情变得美好之前尽早发现问题。这可以帮助项目进行得更加顺利。

## 风险管理和问题解决

高级开发人员可以定义风险，可以通过应用设计模式提炼复杂的问题，并且可以根据过去的经验独立解决不同的问题。

## 提问

伟大的开发者想知道一切。他们不介意问问题，即使这些问题听起来非常简单。这些问题可能是技术问题，也可能是业务相关问题。

理解业务需求有助于他们创建更好的代码！他们不怕问问题，因为他们对自己的能力有信心。

## 尽可能将逻辑排除在数据库之外

这一点取决于您正在构建的应用程序的类型，并且只有在不会影响性能的情况下。

他们知道将数据库查询保持在简单的 CRUD 操作上。

> C **创建、读取(又名检索)、更新和删除**

然后，业务逻辑层应该将这些整合在一起。这有助于开发人员知道在哪里寻找业务逻辑。如果数据库查询和代码中有逻辑，这很快就会变得混乱！

## 吻

> **保持简单愚蠢**

他们知道保持代码简单是最好的办法。即使这意味着有时会创建更多的代码行。你会看到许多较弱的开发人员创建如下的一行程序。

```
return dir.Keys.Any(k => k >= limit) ? dir.First(x => x.Key >= limit).Value : dir[dir.Keys.Max()];
```

这通常是有效的，但是阅读起来却非常困难！

# 结论

这是我每天看到伟大的开发者做的事情。你将会看到它们中的许多与实际的编码无关，而是过程以及它们如何处理任务。我敢肯定还有很多要添加到这个列表中。我希望你喜欢阅读！