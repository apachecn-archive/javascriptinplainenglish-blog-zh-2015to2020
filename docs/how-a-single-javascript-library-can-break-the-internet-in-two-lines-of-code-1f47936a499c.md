# 一个 JavaScript 库如何用两行代码就能攻破互联网

> 原文：<https://javascript.plainenglish.io/how-a-single-javascript-library-can-break-the-internet-in-two-lines-of-code-1f47936a499c?source=collection_archive---------4----------------------->

## 以及从这个和以前的案例中学到了什么

![](img/57fcd14fab31d7230bf03fe7607f0b68.png)

Photo by [Sarah Kilian](https://unsplash.com/@rojekilian?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

几乎每个开发 JavaScript 的人都知道 2016 年的“未发布灾难”，一名开发人员[从 NPM 撤回了他所有的库，并破坏了互联网](https://www.theregister.co.uk/2016/03/23/npm_left_pad_chaos/)。如果你从来没有听说过它，读一读吧，我们所依赖的东西是多么的脆弱，这真令人着迷。

然而，这个故事是关于一个更近的案例，四月的“泄密灾难”。这篇文章的作者实际上在媒体上发表了一篇关于这个案件[的很好的事后分析，我强烈建议你阅读那篇文章。](https://medium.com/javascript-in-plain-english/is-promise-post-mortem-cab807f18dcc)

也有新闻文章([这一篇](https://www.zdnet.com/article/another-one-line-npm-package-breaks-the-javascript-ecosystem/)举例)描述实际问题，但总结一下:

isPromise 是一个 JavaScript 库，在数百万个项目中直接或间接使用，当一个错误的更新破坏了它时，许多其他程序会直接响应。这包括像 Angular，Firebase 和许多其他的大公司。

# 固定您的版本号并手动检查升级

虽然这对于像 2016 年那样的完全不公开没有任何作用，但它可以完全防止这种情况。这正是版本锁定的目的，你告诉 NPM 你想要哪个确切的版本，只有当有真正的理由升级时才升级。

当然，只有在经过全面测试后，您才会将更新推送到您自己的服务器上。

这就产生了相反的问题，每当有一个安全更新修复了不一定出现在每个人的雷达上的关键漏洞时——但我觉得这可以通过警告和例如 Github 的仓库漏洞扫描来规避。

没有版本控制，你就把对你代码的完全控制权交给了互联网上的陌生人，通过版本控制，你可以用你的自由换回来，并付出额外的责任。由于在许多包和程序的构建阶段经常出现多少警告，很容易漏掉一些，这是将警告视为错误的一个很好的理由——但那完全是另一个话题了。我觉得从长远来看，版本锁定带来的麻烦最少。

# 依赖是危险的捷径

长期以来，科技世界已经变得太大，以至于无法自己构建一切，一切都以这样或那样的方式依赖于其他事物。也就是说，“我真的需要导入这个吗？”这个问题是有价值的—有问题的包归结起来只有两行代码。

也就是说，这两行代码非常复杂，包括错误检查和 bool 类型转换，可以很容易地扩展到更多行代码中——有时您会爱上现代语法。

所以这总是一个权衡——如果你开发非常重要的应用程序，就值得更彻底地考虑这个问题。在业余爱好水平的项目中，你可能会花几个小时处理一个坏的构建——但是如果这是其他人工作所依赖的东西，你很快就会浪费大量的时间和金钱，甚至可能产生威胁生命的问题。

有人还记得华盛顿州 911 服务中断是由一个路由呼叫的小服务器引起的吗？

# 这是一个巨大的攻击媒介

虽然这可能是显而易见的，但也应该特别注意:如果有人设法将任何一种未被检测到的后门程序溜进包管理器更新中，我们可以肯定成千上万的项目将自愿导入该代码。

再次强调:随着互联网和技术世界的发展，没有真正的方法来检查所有的东西，尤其是那些你的依赖关系所依赖的东西。

我希望大公司项目中使用的直接依赖关系在升级之前得到验证，但我也在 IT 部门工作过，知道事情经常被忽略，直到出了问题——这可能为时已晚。

# 代码的重要部分可能在任何时候变得不可维护

根据我最近读到的一篇文章，CoreJS 的维护者刚刚[因车辆过失杀人而入狱](https://www.theregister.co.uk/2020/03/26/corejs_maintainer_jailed_code_release/)——使得他的图书馆无人维护。

还有汉斯·赖泽，他[在构建了一个包含在 Linux 内核中的文件系统后，因公然谋杀](https://en.wikipedia.org/wiki/Hans_Reiser)而入狱。

虽然这些都是制造新闻的案例，但总是值得考虑您导入的代码背后的人:他们是人，可以对他们的代码做或不做他们想做的事情。

这可能会造成一个大问题，也许不是一开始，但一旦你需要升级或加固组件，而没有人在另一端更新或修复任何东西，这肯定会造成问题。这就是为什么福克斯被创造出来，然后由一个人来维护，这只是把问题转移给下一个人。

# 归根结底，包管理器仍然是天赐之物

如果没有包管理器、库和标准化代码，任何从事编程或 IT 工作的人都不会有今天的成就。

它有自己的问题、怪癖和明显的危险，但从好的方面来看，它每周——实际上是每天——为我们节省了几个小时的时间，并将整个世界提前了几光年。

所有这些在 netlify 上的静态网站的一键安装，数以千计的初学者项目和你曾经建立的几乎任何东西——它们都依赖于进口的第三方代码。

我希望这篇文章能让你思考我们的科技世界到底有多脆弱，即使每个人都尽了最大努力，事情还是会变得不可收拾。

## **用简单英语写的便条**

你知道我们推出了一个 YouTube 频道吗？我们制作的每个视频都旨在教给你一些新的东西。点击 [**点击**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw) 查看我们，并确保订阅该频道😎