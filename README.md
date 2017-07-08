# 图解 React

> 「图解 React」翻译自 [Under-the-hood-ReactJS](https://github.com/Bogdan-Lyashenko/Under-the-hood-ReactJS)

<em> This repository contains an explanation of inner work of ReactJS. In fact, I was debugging through the entire code base and put all the logic on visual block-schemes, analyzed them, summarized and explained main concepts and approaches. I've already finished with Stack version and now I work with the next, Fiber version.  </em>
**这个代码库包含对 React
内部机制的解释。事实上，我是通过调试整个代码库来梳理并画出逻辑流程图，然后分析它们，总结和解释主要概念和方法的。目前我已经完成了
Stack 版本，Fiber 版本正在进行中。**

>> Read in the best format from [github-pages website](https://bogdan-lyashenko.github.io/Under-the-hood-ReactJS/).
>> 推荐阅读方式：[github-pages website](http://ahonn.github.io/Under-the-hood-ReactJS-CN/)

> Feel free to open an issue regarding any ideas you have to make it better.
> 如果你有任何好想法，请随时提出。

Each scheme is clickable and can be opened in a new tab, use that to zoom it and be able to read from it. Keep the article and a scheme you are reading about at that moment in separate windows (tabs), that will help to match text and code flow easier.
每个流程图都可以双击在新的标签页打开，并通过缩放更好的阅读。保持文章与流程图在不同的窗口（或标签）中打开，有助于快速匹配文章内容与代码。

We are gonna talk here about both ReactJS versions, current one with Stack reconciler and the next one with Fiber (as you probably know, the next version of ReactJS will be released soon), so, you can understand better how current React works and appreciate huge achievements on React-Fiber.  We use React v15.4.2 for explaining how ‘legacy React’ works and React v16.*.*** for ‘Fiber’. Let’s start from old (I have fun to say that) stack version.
我们将在这里进行 React 版本相关的讨论，目前有正在使用的 Stack 协调器版本，以及使用 Fiber 的下个版本（你可能知道下个版本的 React
即将发布），所以你可以很好的了解 React 的工作原理，以及欣赏 React-Fiber 的伟大成就。我们将使用 React v15.4.2
版本来解释旧 React 的工作原理，‘Fiber’ 版本则使用 React v16.*.*** 版本。让我们开始旧 Stack 版本之旅。


## Stack reconciler
## Stack 协调器
[![](./stack/images/intro/all-page-stack-reconciler-25-scale.jpg)](./stack/images/intro/all-page-stack-reconciler.svg)

The entire scheme is divided into 15 parts, let's get started.
整个流程图分为 15 个部分，让我们开始吧。

* [Intro](./stack/book/Intro.md)
* [Part 0](./stack/book/Part-0.md)
* [Part 1](./stack/book/Part-1.md)
* [Part 2](./stack/book/Part-2.md)
* [Part 3](./stack/book/Part-3.md)
* [Part 4](./stack/book/Part-4.md)
* [Part 5](./stack/book/Part-5.md)
* [Part 6](./stack/book/Part-6.md)
* [Part 7](./stack/book/Part-7.md)
* [Part 8](./stack/book/Part-8.md)
* [Part 9](./stack/book/Part-9.md)
* [Part 10](./stack/book/Part-10.md)
* [Part 11](./stack/book/Part-11.md)
* [Part 12](./stack/book/Part-12.md)
* [Part 13](./stack/book/Part-13.md)
* [Part 14](./stack/book/Part-14.md)



## Fiber
1. [Intro](./fiber/book/Intro.md) [TODO]
