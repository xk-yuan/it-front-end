
```
[官网]

	: https://reactjs.org/
	: https://www.reactjscn.com/
	: https://react.docschina.org/
  
  : https://github.com/facebook/react/

[文档]

	: https://react.docschina.org/docs/getting-started.html

// https://www.w3cschool.cn/react/
// https://www.runoob.com/react/react-tutorial.html
// http://caibaojian.com/react/
// http://shouce.jb51.net/react/thinking-in-react.html
//
// http://www.react-china.org/
// http://caibaojian.com/vue-vs-react.html
// http://www.yyyweb.com/4600.html
// https://www.jianshu.com/p/bb20211e8c68

	: react , js 的 UI 库

  : React 认为渲染逻辑本质上与其他 UI 逻辑内在耦合, 
  比如，在 UI 中需要绑定处理事件、在某些时刻状态发生变化时需要通知到 UI,
  以及需要在 UI 中展示准备好的数据。
  
  : React 并没有采用将标记与逻辑进行分离到不同文件这种人为地分离方式, 
  而是通过将二者共同存放在称之为“组件”的松散耦合单元之中，来实现关注点分离

  : React是单向的从数据到视图的渲染，非双向数据绑定

  : 不直接操作DOM对象，而是通过虚拟DOM通过diff算法以最小的步骤作用到真实的DOM上
  
  : React 的核心思想是：封装组件。 各个组件维护自己的状态和 UI，当状态变更，自动重新渲染整个组件。
  
  : 核心概念 - 组件、JSX、虚拟DOM (Virtual DOM)、数据流 (Data Flow, 单向数据绑定)

//
// react4 + react-redux + react-router
// https://segmentfault.com/a/1190000016052564?utm_source=tag-newest
// https://segmentfault.com/a/1190000016661311
// https://segmentfault.com/a/1190000016342792

```

    React ，起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设Instagram 的网站。并于 2013年5月开源。

    随着该项目不断壮大，其从最早的 UI引擎变成了一整套前后端通吃的 Web App 解决方案。衍生的 React Native 项目，目标更是宏伟，希望用写 Web App 的方式去写 Native App。

    其主要用于构建UI。你可以在React里传递多种类型的参数，如声明代码，帮助你渲染出UI、也可以是静态的HTML DOM元素、也可以传递动态变量、甚至是可交互的应用组件。

### 特点

```
[声明式设计]

	: 采用声明范式，可以轻松描述应用。

[高效]

	: 通过对DOM的模拟，最大限度地减少与DOM的交互。

[灵活]

	: 可以与已知的库或框架很好地配合

[JSX]

	: JSX 是 JavaScript 语法的扩展。React 开发不一定使用 JSX ，但我们建议使用它。

[组件]

	: 通过 React 构建组件，使得代码更加容易得到复用，能够很好的应用在大项目的开发中。

[单向响应的数据流]

	: 实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单。

```

