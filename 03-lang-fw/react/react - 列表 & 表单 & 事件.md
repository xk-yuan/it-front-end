### 列表

```
[列表]

	: 渲染多个组件
  
// 通过 map 渲染
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);

ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);

	: 基础列表组件

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);

	: key 帮助 React 识别哪些元素改变了，比如被添加或删除
  // key 会传递信息给 React ，但不会传递给你的组件
  // key 只是在兄弟节点之间必须唯一

// 创建一个元素时，必须包括一个特殊的 key 属性
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);

	: 用 key 提取组件, 元素的 key 只有放在就近的数组上下文中才有意义

function ListItem(props) {
  // 正确！这里不需要指定 key：
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // 正确！key 应该在数组的上下文中被指定
    <ListItem key={number.toString()} value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

### 表单

```
[表单]

	: 表单元素的工作方式和其他的 DOM 元素有些不同，这是因为表单元素通常会保持一些内部的 state

// 此表单具有默认的 HTML 表单行为，即在用户提交表单后浏览到新页面
<form>
  <label>
    名字:
    <input type="text" name="name" />
  </label>
  <input type="submit" value="提交" />
</form>

	: 受控组件
  // 表单元素（如<input>、 <textarea> 和 <select>）之类的表单元素通常自己维护 state
  //  React 中，可变状态（mutable state）通常保存在组件的 state 属性中，并且只能通过使用 setState()来更新
  // 染表单的 React 组件还控制着用户输入过程中表单发生的操作。被 React 以这种方式控制取值的表单输入元素就叫做“受控组件”
  // 对于受控组件来说，每个 state 突变都有一个相关的处理函数

// 表单元素上设置了 value 属性，因此显示的值将始终为 this.state.value，这使得 React 的 state 成为唯一数据源
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('提交的名字: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          名字:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="提交" />
      </form>
    );
  }
}

// --
handleChange(event) {
  this.setState({value: event.target.value.toUpperCase()});
}

	: textarea 标签
// <textarea> 使用 value 属性代替。这样，可以使得使用 <textarea> 的表单和使用单行 input 的表单非常类似
// this.state.value 初始化于构造函数中，因此文本区域默认有初值
class EssayForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: '请撰写一篇关于你喜欢的 DOM 元素的文章.'
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('提交的文章: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          文章:
          <textarea value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="提交" />
      </form>
    );
  }
}

	: select 标签
  // <select> 创建下拉列表标签
	// React 并不会使用 selected 属性，而是在根 select 标签上使用 value 属性

class FlavorForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: 'coconut'};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('你喜欢的风味是: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          选择你喜欢的风味:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="grapefruit">葡萄柚</option>
            <option value="lime">柠檬</option>
            <option value="coconut">椰子</option>
            <option value="mango">芒果</option>
          </select>
        </label>
        <input type="submit" value="提交" />
      </form>
    );
  }
}

	: input 标签

	: 处理多个输入
  // 给每个元素添加 name 属性，并让处理函数根据 event.target.name 的值选择要执行的操作

class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          参与:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        

        <label>
          来宾人数:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}

	: 受控输入空值
  // 在受控组件上指定 value 的 prop 可以防止用户更改输入
  // 如果指定了 value, 但输入仍可编辑，则可能是意外地将value 设置为 undefined 或 null

//输入最初被锁定，但在短时间延迟后变为可编辑
ReactDOM.render(<input value="hi" />, mountNode);

setTimeout(function() {
  ReactDOM.render(<input value={null} />, mountNode);
}, 1000);

	: 受控组件的替代品
  // 使用受控组件会很麻烦，因为你需要为数据变化的每种方式都编写事件处理函数，并通过一个 React 组件传递所有的输入 state

```

### 事件

```
[事件处理]

	: 元素的事件处理和 DOM 元素的很相似, 但是有一点语法上的不同
  // React 事件的命名采用小驼峰式（camelCase），而不是纯小写
  // 使用 JSX 语法时你需要传入一个函数作为事件处理函数，而不是一个字符串
  // 不能通过返回 false 的方式阻止默认行为。你必须显式的使用 preventDefault 

// 传入事件函数
<button onClick={activateLasers}>
  Activate Lasers
</button>

//
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}

	: 一般不需要使用 addEventListener 为已创建的 DOM 元素添加监听器, 事件处理函数声明为 class 中的方法
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // 为了在回调中使用 `this`，这个绑定是必不可少的
    // 在 JavaScript 中，class 的方法默认不会绑定 this。
    // 未绑定 this.handleClick 并把它传入了 onClick, 当调用这个函数的时候 this 的值为 undefined
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle/>,
  document.getElementById('root')
);

	: 事件处理程序传递参数

// 箭头函数和 Function.prototype.bind 
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>

```

```
//
var HelloMessage = React.createClass({
  getInitialState: function() {
    return {value: 'Hello W3CSchool!'};
  },
  
  handleChange: function(event) {
    this.setState({value: event.target.value});
  },
  // 输入框 input 值value = {this.state.data}。在输入框值发生变化时我们可以更新 state
  // 使用 onChange 事件来监听 input 的变化，并修改 state
  render: function() {
    var value = this.state.value;
    return 
      <div>
        <input type="text" value={value} onChange={this.handleChange} /> 
        <h4>{value}</h4>
      </div>;
  }
});

ReactDOM.render(
  <HelloMessage />,
  document.getElementById('example')
);
```

```
// 子组件上使用表单
// onChange 方法将触发 state 的更新并将更新的值传递到子组件的输入框的 value 上来重新渲染界面
// 父组件通过创建事件句柄 (handleChange) ，并作为 prop (updateStateProp) 传递到你的子组件上
var Content = React.createClass({
  render: function() {
    return  <div>
            <input type="text" value={this.props.myDataProp} onChange={this.props.updateStateProp} /> 
            <h4>{this.props.myDataProp}</h4>
            </div>;
  }
});
var HelloMessage = React.createClass({
  getInitialState: function() {
    return {value: 'Hello W3CSchool!'};
  },
  handleChange: function(event) {
    this.setState({value: event.target.value});
  },
  render: function() {
    var value = this.state.value;
    return <div>
            <Content myDataProp = {value} 
              updateStateProp = {this.handleChange}></Content>
           </div>;
  }
});
ReactDOM.render(
  <HelloMessage />,
  document.getElementById('example')
);

// onClick 事件来修改数据
var HelloMessage = React.createClass({
  getInitialState: function() {
    return {value: 'Hello W3CSchool!'};
  },
  handleChange: function(event) {
    this.setState({value: 'W3Cschool教程'})
  },
  render: function() {
    var value = this.state.value;
    return <div>
            <button onClick={this.handleChange}>点我</button>
            <h4>{value}</h4>
           </div>;
  }
});
ReactDOM.render(
  <HelloMessage />,
  document.getElementById('example')
);

// 从子组件中更新父组件的 state 时，你需要在父组件通过创建事件句柄 (handleChange) ，并作为 prop (updateStateProp) 传递到你的子组件上
var Content = React.createClass({
  render: function() {
    return  <div>
              <button onClick = {this.props.updateStateProp}>点我</button>
              <h4>{this.props.myDataProp}</h4>
           </div>
  }
});
var HelloMessage = React.createClass({
  getInitialState: function() {
    return {value: 'Hello W3CSchool!'};
  },
  handleChange: function(event) {
    this.setState({value: 'W3Cschool教程'})
  },
  render: function() {
    var value = this.state.value;
    return <div>
            <Content myDataProp = {value} 
              updateStateProp = {this.handleChange}></Content>
           </div>;
  }
});
ReactDOM.render(
  <HelloMessage />,
  document.getElementById('example')
);
```

