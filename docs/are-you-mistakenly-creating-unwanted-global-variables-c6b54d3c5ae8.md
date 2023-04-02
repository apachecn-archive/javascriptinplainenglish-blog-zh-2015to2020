# 您是否错误地创建了不需要的全局变量？

> 原文：<https://javascript.plainenglish.io/are-you-mistakenly-creating-unwanted-global-variables-c6b54d3c5ae8?source=collection_archive---------3----------------------->

![](img/25a291a681c7c7f9e8ef6ead252075e5.png)

## Javascript 是一种动态编程语言，它为我们提供了很大的灵活性，比如为同一个变量分配不同的数据类型，动态声明变量等等。

但与此同时，它也带来了许多警告，人们很容易忽略这些警告，并且永远不会意识到它的后果。

## 今天我们要谈论的就是这样一个案例，如果不注意的话，它会造成严重的问题。

我们知道 javascript 允许我们动态声明变量，甚至重新声明它。但是你有没有想过，如果你在声明一个变量之前没有放上一个 var/let/const 关键字会怎么样？

## 让我们从一段代码开始

在上面的代码片段中，我们有一个名为`iAmUsefulFn()`的随机函数，它接受一个参数。

现在仔细看看函数的内部。我们声明了一个名为`name`的变量，没有任何关键字，添加了一个带有`.`的参数，并将其存储在 name 中。

乍一看，这段代码看起来绝对正常。但实际上，它会在应用程序中引起严重安全和性能问题。原因:

> 在 Javascript 中，没有任何关键字声明的变量(let/const/var)将自动成为一个全局变量，并附加到全局对象上。(浏览器的窗口对象)

所以如果我在窗口对象中查找 name 变量，我能找到它吗？

是的，我会的，它会在里面存储`Shubham.`的值。

```
console.log(window.name) //Shubham.
```

因此，这段代码最大的风险是“乍一看没问题”,但它可能会在您的应用程序中导致意外的错误，并且以后很难调试。除非你有意让它全球化。

## 希望从现在开始，我们在 Javascript 中声明变量时会小心谨慎，并且永远不要忘记加上一个`let/const/var`关键字。

## 完整的代码可以在下面的 Codepen 上试用: