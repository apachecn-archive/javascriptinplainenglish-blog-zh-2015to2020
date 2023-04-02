# 为什么要反应钩子？

> 原文：<https://javascript.plainenglish.io/why-hooks-9cd1fb586b75?source=collection_archive---------2----------------------->

![](img/5c2b53092948b8e8986b4db1d8aff53c.png)

Photo by [Joanna Kosinska](https://unsplash.com/@joannakosinska?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你是一名 React 开发人员，你很难逃避关于 React 钩子的讨论。对于那些不熟悉的人来说，钩子是一系列内置的 React 函数，允许开发人员在功能组件内部的类组件中做他们能做的任何事情。

但是为什么要改变呢？如果类组件可以做我们希望它们做的所有事情——初始化状态、设置状态、访问组件生命周期、创建上下文、调用引用等。—那么我们为什么想要一种方法让我们愚蠢的、表示性的组件也这样工作呢？功能组件有什么特别的？

事实证明，使用钩子给开发人员带来好处有几个原因。第一个是大类组件可能很难处理。从事大型应用程序、集中式、有状态组件的工程师的规模可能会膨胀，通常情况下，相同或相似的逻辑会分布在组件生命周期方法中。第二是方法重用。重用组件方法，尤其是复杂的逻辑，依赖于设计模式，如高阶组件或渲染道具，这反过来要求开发人员重新组织他们的组件层次结构，并可能导致包装器的混乱。最后，类语法对于人类和机器来说都是令人困惑的，并且会偏离 React 试图维护的纯功能设计模式。

那么钩子是如何解决这些问题的呢？

# 组件大小

当涉及到组件的规模时，钩子通过 [useEffect](https://reactjs.org/docs/hooks-effect.html) 抽象出生命周期方法中的许多重复功能，并通过个性化的 [useState](https://reactjs.org/docs/hooks-state.html) 调用简化状态初始化。例如，一个 useEffect 钩子可以完成 3 个生命周期方法的工作:componentDidMount、componentDidUpdate 和 componentWillUnmount。通过指定一个可选的依赖数组，您可以告诉 useEffect 在指定的状态引用中查找变化，并再次运行该效果——实际上相当于 componentDidUpdate。通过指定一个空的依赖数组，您告诉 useEffect 只运行一次。当组件从 DOM 中移除，并且您需要执行一些数据清理——比如清除一个间隔或阻止一个 api 调用——您可以在一个将在 unmount- componentWillUnmount 上运行的 return 语句中给 useEffect 一个回调。所有这些工作都可以通过一个 useEffect 调用来完成，这使得它成为解决副作用的一个极其强大的方法！

# 方法重用

当涉及到在我们的应用程序中的其他地方重用组件逻辑时，我们概括这些场景的传统方式是使用渲染道具或 hoc(高阶组件)。

渲染道具的工作方式是将一个定制的回调函数和个性化的 JSX 作为道具传递给我们的组件。当我们希望相同的数据可以在我们呈现的组件的多个实例中重用时，我们使用这个方法。例如，如果我们想通过一个组件跟踪我们的鼠标位置，但想对该数据做不同的事情(比如在一个

标签而不是

# 标签中显示位置),我们可以通过用定制的 JSX 指定渲染道具来实现。

hoc(高阶组件)通过创建包装组件或返回包装组件的函数来工作，该包装组件给予包装组件对某些数据或功能的访问。如果多个组件在做类似但略有不同的工作，比如从相同的源获取一些数据，但使用不同的方法，我们会希望使用这种方法。想想 Redux 的 connect()函数，它将包装的组件连接到我们的存储。这里可能需要连接多个组件，但是对状态和分派方法有不同的需求。因此，我们可以为我们的 connect HOC 提供定制的 mapStateToProps 和 mapDispatchToProps 函数，以便为我们的包装组件提供个性化的数据。

虽然这些模式对于类组件非常有效，但是它们也有缺点。特别是，它们要求开发人员重写组件层次结构，并可能导致第九层包装地狱。钩子的替代方法是允许我们的钩子调用以[定制钩子](https://reactjs.org/docs/hooks-custom.html)的形式跨组件共享。定制钩子只是可组合的函数，可以像其他函数一样在组件间导出和共享。所谓可组合，我们指的是获取多个部分(如 useState 和 useEffect 调用)，将它们组合成一个可重用的模式，并将它们抽象成各自独立的函数的能力。这种模式在类组件中是不可能的，因为像获取数据或实例化状态这样简单的事情不能与调用它们的类方法分开。

# 表现和困惑

最后，对于类组件内部的性能有一些小的担心。在 [React Conference 2018](https://www.youtube.com/watch?v=dpw9EHDh2bM) 上，React Hooks 亮相的时候就指出，类组件无论是机器还是人都很难理解。由于类语法只是 JavaScript 的原型继承的语法化，类的工作方式与其他编程语言不同。因此，React 团队已经注意到在生产构建中缩小类组件的问题，并且在实现热模块重载时存在不一致性。此外，对于工程师来说，尤其是那些不熟悉类语法的人，理解“this”关键字的绑定是如何工作的，或者理解其他类的细微差别，比如在构造函数中调用 super()的目的，可能会很困难。

因为钩子允许我们在功能组件中使用所有相同的类组件功能，所以我们能够提高 React 代码的性能。此外，钩子有一个清晰的语法，不仅更符合 React 的纯功能设计，也更符合它们对 JavaScript 的关注。React 与 Vue 等其他基于组件的前端库的主要区别之一是，它通过 JSX 和 css 模块耦合 html、css 和 JavaScript。这意味着，如果您是 JavaScript 专家，那么您就是 React(给出或获取实现细节)专家，而 Vue 的模板结构依赖于在 HTML、CSS 和 JS 之间分割文件，就像过去的 jQuery 和普通 JavaScript DOM 操作一样。

虽然功能组件的性能略有提升是好事，但是性能不应该是使用钩子的主要原因。钩子不会添加 React 中已经不存在的任何功能。它的主要目的只是将功能组件提升到与类组件相同的级别，从而通过更干净、更易维护的代码、跨组件的更好的方法重用、使用状态、生命周期方法的更简单、更具声明性的方式以及大量其他 React 功能(如引用、记忆化、简化器和上下文)来提供更好的 DX(开发人员体验)。

也就是说，我有同事发现钩子在概念上难以理解，尤其是在理解使用效果、使用状态或使用上下文时。例如，很难看出如何将生命周期方法中不同的逻辑组合成一个单一的函数调用。所以最近，我和一群工程师创建了一个名为 [Hookd](https://github.com/oslabs-beta/hookd) 的 CLI 模板工具，用钩子将类组件即时转换成功能组件。我们刚刚发布了我们的 Alpha 版本，希望有贡献者和反馈。如果下载一个 CLI 不是你的风格，我们也有一个[客户端](https://www.hookd.dev/)，在那里你可以 c/p 你的组件来找到钩子的等价物。

# 清理你的代码，清理你的思想

最终，使用钩子似乎不仅仅是开发人员的一种时尚。它允许开发人员清理他们的代码，从而清理他们的思想。不应该低估干净的声明性代码有助于生成更多无错误、模块化和可维护的应用程序的重要性。在机器开始为我们编码之前，我们一直处于非常人性化的约束之下，遵循对我们以及我们必须与之交流的其他人有意义的逻辑。