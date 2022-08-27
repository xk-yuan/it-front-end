### 元素

```
[元素]

	: 元素是构成 React 应用的最小砖块, 组件是由元素构成的
  
  : 元素渲染为 DOM, 由 React DOM 管理
  // 素渲染到根 DOM 节点中，只需把它们一起传入 ReactDOM.render()
  // const element = <h1>Hello, world</h1>;
  // ReactDOM.render(element, document.getElementById('root'));
  
  : React 元素是不可变对象。一旦被创建，你就无法更改它的子元素或者属性。
  // 更新 UI 唯一的方式是创建一个全新的元素，并将其传入 ReactDOM.render()
  // 调用 ReactDOM.render() 来修改我们想要渲染的元素
  // React DOM 会将元素和它的子元素与它们之前的状态进行比较, 并只会进行必要的更新来使 DOM 达到预期的状态

// 计时器
function tick() {
  // 创建元素
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  // 渲染元素
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);

```

### 组件

```
[组件]

	: 组件允许你将 UI 拆分为独立可复用的代码片段，并对每个片段进行独立构思
  
  : 组件，从概念上类似于JS函数, 它接受任意的入参(“props”), 并返回用于描述页面展示内容的 React 元素
  
  : 定义组件最简单的方式就是编写 JavaScript 函数, 被称为“函数组件”, 其本质上就是 JavaScript 函数
  
  : 组件名称必须以大写字母开头, React 会将以小写字母开头的组件视为原生 DOM 标签


// React.createClass 方法用于生成一个组件类
var HelloMessage = React.createClass({
  render: function() {
    return <h1>Hello World！</h1>;
  }
});

ReactDOM.render(
  <HelloMessage />,
  document.getElementById('example')
);

// 向组件传递参数, 可以使用 this.props 对象
var HelloMessage = React.createClass({
  render: function() {
    return <h1>Hello {this.props.name}</h1>;
  }
});

ReactDOM.render(
  <HelloMessage name="W3CSchool" />,
  document.getElementById('example')
);


// -- 定义组件
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
// -- ES6 class 语法定义组件
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

	: React 元素可以是 DOM 标签, 也可以是用户自定义的组件
  // const element = <div />;
  // const element = <Welcome name="Sara" />;
  //  React 元素为用户自定义组件时, 它会将 JSX 所接收的属性转换为单个对象传递给组件, 称之为 “props”

// -- 定义组件
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// -- 定义元素
const element = <Welcome name="Sara" />;
// -- 渲染元素
ReactDOM.render(
  element,
  document.getElementById('root')
);

	: 组合组件, 组件可以在其输出中引用其他组件, 用同一组件来抽象出任意层次的细节

// --
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);

	: 将组件拆分为更小的组件, 复合组件

function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar" src={props.author.avatarUrl} alt={props.author.name}
        />

        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}

// 提取 Avatar 组件, Avatar 不需知道它在 Comment 组件内部是如何渲染的
function Avatar(props) {
  return (
    <img className="Avatar" src={props.user.avatarUrl} alt={props.user.name}
    />
  );
}

// 提取 UserInfo 组件，该组件在用户名旁渲染 Avatar 组件
// 从组件自身的角度命名 props，而不是依赖于调用组件的上下文命名
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        ...
      </div>
      ...
    </div>
  );
}

// 提取 UserInfo 组件, 该组件在用户名旁渲染 Avatar 组件
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}

function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      ...
    </div>
  );
}



```

#### props

```
[props 属性]

	: Props , 组件无论是使用函数声明还是通过 class 声明, 都决不能修改自身的 props
  // 所有 React 组件都必须像纯函数一样保护它们的 props 不被更改
  
  : state 和 props 主要的区别在于 props 是不可变的，而 state 可以根据与用户交互来改变
  

  
  : 子组件只能通过 props 来从父组件中传递数据, 数据自顶向下流动

// React.PropTypes 提供很多验证器 (validator) 来验证传入数据是否有效
// 当向 props 传入无效数据时，JavaScript 控制台会抛出警告
// React.PropTypes 在 React v15.5 版本后已经移到了 prop-types 库。
// <script src="https://cdn.bootcss.com/prop-types/15.6.1/prop-types.js"></script>
```

#### state

```
[state 状态]

	: 组件看成是一个状态机 (State Machines),实现不同状态渲染 UI, 让用户界面和数据保持一致
  : 只需更新组件的 state，然后根据新的 state 重新渲染用户界面, 而不需要操作 DOM

  : state
  // State 与 props 类似, 但是 state 是私有的，并且完全受控于当前组件
  // 构造函数是唯一可以给 this.state 赋值的地方
  // 不要直接修改 State, 使用 setState()
  // State 的更新可能是异步的
  // State 的更新会被合并
  // 数据是向下流动, 不管是父组件或是子组件都无法知道某个组件是有状态的还是无状态
  // 组件可以选择把它的 state 作为 props 向下传递到它的子组件中

// 
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);

  : 函数组件转换成 class 组件
  // 创建一个同名的 ES6 class，并且继承于 React.Component。
  // 添加一个空的 render() 方法。
  // 将函数体移动到 render() 方法之中。
  // 在 render() 方法中使用 this.props 替换 props。
  // 删除剩余的空函数声明

// Clock 组件被定义为 class，而不是函数
// 每次组件更新时 render 方法都会被调用, 
// 但只要在相同的 DOM 节点中渲染 <Clock /> , 就仅有一个 Clock 组件的 class 实例被创建使用
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

	: class 组件中添加局部的 state
	// render() 方法中的 this.props.date 替换成 this.state.date
  // 添加一个 class 构造函数，然后在该函数中为 this.state 赋初值
  // 通过以下方式将 props 传递到父类的构造函数中
  // Class 组件应该始终使用 props 参数来调用父类的构造函数

class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

//
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);

```

#### 生命周期 & API

![image.png](https://cdn.nlark.com/yuque/0/2019/png/210477/1577713362256-50cc0f1d-0a67-456a-a55f-2e9306d577d5.png#align=left&display=inline&height=434&name=image.png&originHeight=635&originWidth=1095&size=68615&status=done&style=none&width=746)

```
[生命周期方法]

	: 生命周期函数，又叫钩子函数，它能响应不同的状态
  
  // -- 生命周期状态
  : Mounting    已插入真实 DOM
	: Updating    正在被重新渲染
	: Unmounting  已移出真实 DOM

	// -- 生命周期方法
	: componentWillMount    在渲染前调用,在客户端也在服务端
  
	: componentDidMount   在第一次渲染后调用, 方法会在组件已经被渲染到 DOM 中后运行 (只在客户端)
  // 之后组件已经生成了对应的DOM结构，可以通过this.getDOMNode()来进行访问
  // 如果你想和其他JavaScript框架一起使用
  // 可以在这个方法中调用setTimeout, setInterval或者发送AJAX请求等操作(防止异部操作阻塞UI)。

  : componentWillReceiveProps 在组件接收到一个新的prop时被调用
  // 这个方法在初始化render时不会被调用。

  : shouldComponentUpdate 返回一个布尔值, 在组件接收到新的props或者state时被调用
  // 在初始化时或者使用forceUpdate时不被调用, 可以在你确认不需要更新组件时使用。

  : componentWillUpdate  在组件接收到新的props或者state但还没有render时被调用
  // 在初始化时不会被调用

  : componentDidUpdate 在组件完成更新后立即调用, 在初始化时不会被调用。

  : componentWillUnmount 在组件从 DOM 中移除的时候立刻被调用。


class Clock extends React.Component {
  constructor...

  componentDidMount() {
  }

  componentWillUnmount() {
  }

  render()...
}

// https://react.docschina.org/docs/react-component.html

[组件 API]

	: setState      设置状态
  // setState(object nextState[, function callback])
  // nextState, 将要设置的新状态, 该状态会和当前的state合并
	// callback, 可选参数, 回调函数。该函数会在setState设置成功, 且组件重新渲染后调用。
	// 合并nextState和当前state, 并重新渲染组件。setState是React事件处理函数中和请求回调函数中触发UI更新的主要方法。
  // 不能在组件内部通过this.state修改状态, 因为该状态会在调用setState()后被替换
  // setState()并不会立即改变this.state，而是创建一个即将处理的state。setState()并不一定是同步的，为了提升性能React会批量执行state和DOM渲染。
  // setState()总是会触发一次组件重绘，除非在shouldComponentUpdate()中实现了一些条件渲染逻辑。
  
  : setProps      设置属性
  // setProps(object nextProps[, function callback])
  // nextProps，将要设置的新属性，该状态会和当前的props合并
	// callback，可选参数，回调函数。该函数会在setProps设置成功，且组件重新渲染后调用。
	// 设置组件属性，并重新渲染组件。
  // props相当于组件的数据流，它总是会从父组件向下传递至所有的子组件中。
  // 更新组件，我可以在节点上再次调用React.render()，也可以通过setProps()方法改变组件属性，触发组件重新渲染。
  
  : replaceState  替换状态
  // replaceState(object nextState[, function callback])
  // nextState，将要设置的新状态，该状态会替换当前的state。
	// callback，可选参数，回调函数。该函数会在replaceState设置成功，且组件重新渲染后调用。
	// replaceState()方法与setState()类似，但是方法只会保留nextState中状态，原state不在nextState中的状态都会被删除。

  : replaceProps  替换属性
  // replaceProps(object nextProps[, function callback])
  // nextProps，将要设置的新属性，该属性会替换当前的props。
	// callback，可选参数，回调函数。该函数会在replaceProps设置成功，且组件重新渲染后调用。
	// replaceProps()方法与setProps类似，但它会删除原有
  
  : forceUpdate   强制更新
  // forceUpdate([function callback])
  // callback，可选参数，回调函数。该函数会在组件render()方法调用后调用。
  // 会使组件调用自身的render()方法重新渲染组件，组件的子组件也会调用自己的render()。
  // 组件重新渲染时，依然会读取this.props和this.state，如果状态没有改变，那么React只会更新DOM
  // 适用于this.props和this.state之外的组件重绘
  // 通过该方法通知React需要调用render()
  // 一般来说，应该尽量避免使用forceUpdate()，而仅从this.props和this.state中读取状态并由React触发render()调用
  
  : findDOMNode   获取DOM节点
  // DOMElement findDOMNode()
  // 如果组件已经挂载到DOM中，该方法返回对应的本地浏览器 DOM 元素
  // 当render返回null 或 false时，this.findDOMNode()也会返回null
  
  : isMounted     判断组件挂载状态
  // bool isMounted()
  // 判断组件是否已挂载到DOM中。可以使用该方法保证了setState()和forceUpdate()在异步场景下的调用不会出错

```

