```

[生命周期函数图]

	: https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/

```


![image.png](../../imgs/1594777842608-1ad57486-d4e7-4a1d-a257-c5fc391fee66.png#align=left&display=inline&height=422&margin=%5Bobject%20Object%5D&name=image.png&originHeight=422&originWidth=1107&size=49516&status=done&style=none&width=1107)


### 挂载


> 当组件实例被创建并插入 DOM 中时，其生命周期调用顺序如下
> 1. constructor()
> 1. static getDerivedStateFromProps()
> 1. render()
> 1. componentDidMount()



```
[constructor()]

- 如果不初始化 state 或不进行方法绑定，则不需要为 React 组件实现构造函数。
// 为 React.Component 子类实现构造函数时，应在其他语句之前前调用 super(props)
// 不要调用 setState() 方法

- 构造函数适用的情况
1. 通过给 this.state 赋值对象来初始化内部 state
2. 为事件处理函数绑定实例

[componentDidMount()]

- 在组件挂载后（插入 DOM 树中）立即调用, 依赖于 DOM 节点的初始化应该放在这里。
// 如需通过网络请求获取数据，此处是实例化请求的好地方。
// 可以在此处直接调用 setState(), 将触发额外渲染, 但此渲染会发生在浏览器更新屏幕之前。
// 保证了即使在 render() 两次调用的情况下，用户也不会看到中间状态, 但会导致性能问题
// 通常应该在 constructor() 中初始化 state, 如果你的渲染依赖于 DOM 节点的大小或位置, 可以试用

```



### 更新


> 当组件的 props 或 state 发生变化时会触发更新。组件更新的生命周期调用顺序如下
> 1. static getDerivedStateFromProps()
> 1. shouldComponentUpdate()
> 1. render()
> 1. getSnapshotBeforeUpdate()
> 1. componentDidUpdate()



```
[componentDidUpdate(prevProps, prevState, snapshot)]

- 会在更新后会被立即调用。但是首次渲染不会执行此方法。

```


```
[shouldComponentUpdate(nextProps, nextState)]

- 根据 shouldComponentUpdate() 的返回值, 判断组件的输出是否受当前 state 或 props 更改的影响。
// 默认行为是 state 每次发生变化组件都会重新渲染。
// 当 props 或 state 发生变化时，会在渲染执行之前被调用。返回值默认为 true。
// 首次渲染或使用 forceUpdate() 时不会调用该方法。
// 不建议在 shouldComponentUpdate() 中进行深层比较或使用 JSON.stringify()。这样非常影响效率，且会损害性能

[static getDerivedStateFromProps(props, state)]

- 在调用 render 方法之前调用，并且在初始挂载及后续更新时都会被调用。
它应返回一个对象来更新 state，如果返回 null 则不更新任何内容

[getSnapshotBeforeUpdate(prevProps, prevState)]

- 在最近一次渲染输出（提交到 DOM 节点）之前调用
// 使得组件能在发生更改之前从 DOM 中捕获一些信息


```


### 卸载


> 当组件从 DOM 中移除时会调用如下方法
> 1. componentWillUnmount()



```
[componentWillUnmount()]

- 组件卸载及销毁之前直接调用, 此方法中执行必要的清理操作
```


### 错误处理


> 当渲染过程，生命周期，或子组件的构造函数中抛出错误时，会调用如下方法
> 1. static getDerivedStateFromError()
> 1. componentDidCatch()



### 其他


> - 额外API
> - setState()
> - forceUpdate()



> - class 属性
> - defaultProps
> - displayName



> - 实例属性
> - props
> - state

