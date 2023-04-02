# TestCafe 中用户角色的权力

> 原文：<https://javascript.plainenglish.io/power-of-user-roles-in-testcafe-b88458baae17?source=collection_archive---------3----------------------->

## 加速您的 testCafe UI 测试

## *避免让你的 UI 测试脚本反复运行相同的登录步骤*

![](img/51a38185284a9e7051673f0283863cda.png)

Photo by [Jake Givens](https://unsplash.com/@jakegivens?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

长时间运行的 UI 测试套件可能会令人沮丧，并可能导致一系列问题，例如

*   **更长的反馈循环:**长时间的执行可能会促使开发团队完全避免使用你的 UI 测试。
*   **耗时的模拟测试:**测试你的测试中的任何变化都会花费更长的时间。
*   **很难说服开发团队将这些集成到 CI 中:**没有人喜欢等待几个小时在 CI 中完成部署，却发现由于前端测试中的错误选择器而失败。

本质上，测试越快，反馈周期越短，越有可能有更多的人使用和信任这些测试。

传统上，当涉及到减少测试执行时间时，我们经常会提出像并行运行测试这样的解决方案，这确实节省了我们的时间，但是还可以做得更多。

**test cafe 中的用户角色有哪些？**

TestCafe 包含一个用户角色机制，允许您模拟用户登录网站的操作。

许多测试场景涉及来自多个用户的活动。TestCafe 允许您隔离验证用户所需的测试操作(例如，输入凭据，单击“登录”)。在测试过程中，您可以通过一个方法调用在用户帐户之间切换。

角色*包含登录特定用户的代码。您可以在测试中为每个用户帐户定义一个角色。*

**为什么要使用角色？**

如今，大多数应用程序都需要用户登录才能访问大部分功能。因此，大多数测试都需要登录。想象一下，有一个包含 200 个测试场景的大型测试套件，您可能需要登录 200 次。这显然要消耗很多时间。

另一个用例可能是，假设您的应用程序具有基于角色的访问。您可能想要编写一些场景来测试某些功能是否可以被允许用户访问。如果您必须在整个测试过程中登录尽可能多的不同用户，您会发现自己在重复登录过程。您的测试套件将会被重复的代码弄得乱七八糟，并且当您在多个场合让用户登录和退出系统时，您的测试将会明显变慢。

使用角色不仅可以解决这样的问题，还可以让你的代码看起来干净，并且可以提高测试的执行速度。

**用户角色的特点:**

*   **基于对象的 API。**认证数据和逻辑存储在一个对象中，需要时容易传递和激活。
*   **单点登录。**当您在同一会话中切换到以前使用的角色时，不会重复登录操作。如果您在每个挂钩之前激活了[中的一个角色，那么在第一次测试之前，登录操作会运行一次。后续测试重用身份验证数据，以便它立即发生。](https://devexpress.github.io/testcafe/documentation/guides/basic-guides/organize-tests.html#test-hooks)
*   **自动返回。**浏览器会自动导航回您切换角色的页面。(如果需要，您可以禁用此行为。)
*   不需要注销。当您切换角色时，认证数据会自动清除。
*   **多重认证支持。**如果您在测试期间登录不同的服务/网站，来自 cookie 和浏览器存储的认证数据会在活动角色中累积。当您在同一测试中切换回该角色时，您将自动登录到所有网站。
*   **匿名角色。**注销所有帐户的内置角色。

**如何创建用户角色？**

使用角色构造函数创建和初始化角色。传递登录页面 URL，并通过输入用户名和密码进行登录。在本例中，我创建了两个角色，一个是管理员，另一个是员工。

如何在你的测试中使用用户角色？

将角色导入到您的测试文件中，并将下面一行添加到您的测试中以触发角色。

```
await t.useRole(roleName)
```

**例 1**

在本例中，有三个测试，每个测试都使用相同的名为“herokuLogin”的用户角色。对于执行的第一个测试，登录只发生一次，其他两次将使用已经创建的会话。

**例二**:

注意，我们在两个测试中都使用了' *roleEmployee'* 。雇员的登录只发生一次，testCafe 将存储 cookies 和会话相关信息以及保留的 URL。

第二个测试将使用已经创建的会话。因此，员工不需要第二次登录。

此外，在不同的用户角色之间切换非常容易。没有必要注销，因为 testCafe 处理所有开箱即用的东西。这也让你的代码看起来更干净。

更多信息请访问“ [TestCafe 文档](https://devexpress.github.io/testcafe/documentation/guides/advanced-guides/authentication.html#user-roles)

代码可在我的 git [这里](https://github.com/rahulrana1/role_testCafe)获得。如果有任何反馈，请随时联系我。