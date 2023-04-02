# 对错误边界做出反应:让用户满意

> 原文：<https://javascript.plainenglish.io/react-error-boundaries-keeping-the-user-happy-b00c04833aaa?source=collection_archive---------0----------------------->

## 如何使用 React 更好地处理您未发现的错误

![](img/3112c991b0d1d39bfdbf2433f52ebc7f.png)

为了度过我们的应用程序的用户遇到白屏的日子，这对于开发人员来说可能是一种可怕的体验，但对于用户来说是一种非常令人沮丧的体验，我们需要实现一个系统来捕捉我们的灾难，并给用户一条“快乐的道路”来走。

简介，反应错误界限。

React 错误边界对于我们的前端开发来说是新的，因此这样一个工具的实现将需要更多的思考，不仅仅是它如何影响用户体验，而是这些错误边界将在哪里出现。这个问题的棘手之处在于，从技术上讲，错误可以同时出现在任何地方。一个致命的错误可能很难重现或者一直存在，因此我们可能应该重新考虑代码的完整性。无论如何，我们需要能够优雅地捕捉这些错误，不幸的是，只有当用户从一封讨厌的电子邮件或一个简单的提醒中发现这些错误时，我们才可能意识到这些错误的存在。

根据 [React 文档](https://reactjs.org/docs/error-boundaries.html)，

> 错误边界是 React 组件，它捕捉子组件树中任何地方的 JavaScript 错误，记录这些错误，并显示一个回退 UI，而不是崩溃的组件树。

虽然我在介绍中不止一次提到了用户，但是记住错误边界并不能帮助我们捕获由事件处理程序(如单击按钮或输入更改)导致的错误，这一点很重要。这些错误是通过使用 try/catch 语句以传统方式捕获的。我提到这一点是因为错误边界是特定于渲染、生命周期方法以及它们下面的整个树的构造函数的。

那么，我们如何最好地实现错误边界呢？这个问题没有直接的答案。“视情况而定”可能是我能给出的最好的答案，但是有一些要点需要记住。确定放置误差边界的位置时:

*   确定错误是否会导致应用程序的其他部分崩溃。如果是这种情况，最好在顶层路由中放置一个错误边界，这样只能给用户一个继续使用应用程序的选项:刷新并重试。
*   如果错误出现在不影响应用程序整体体验的独立组件中，最好只包装该组件。

组件与其兄弟或父组件的关系在这里很重要。如果用户的最终目标需要的不仅仅是一个坏组件，我们不希望“组件病毒”传播并对我们的其他组件造成伤害。

最终，我们希望我们的 UI 错误对我们的用户来说尽可能的不引人注目和没有痛苦。

莎拉·基利安在 [Unsplash](https://unsplash.com/search/photos/error?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片