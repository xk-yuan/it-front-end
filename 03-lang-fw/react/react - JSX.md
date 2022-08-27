### JSX

```
[JSX]
    : JSX 是 React 的核心组成部分, 它使用 XML 标记的方式去直接声明界面, 界面组件之间可以互相嵌套
    
  : 一个 JavaScript 的语法扩展, JSX 可以很好地描述 UI 应该呈现出它应有交互的本质形式, 描述用户界面
  
    : JSX 表达式会被转为普通 JavaScript 函数调用，并且对其取值后得到 JavaScript 对象
  
  : JSX 使用大、小写的约定来区分本地组件的类和 HTML 标签
[JSX 表达式]
    : const element = <h1>Hello, world</h1>;
[样式]
    : React 推荐使用内联样式。我们可以使用 camelCase 语法来设置内联样式
var myStyle = {
    fontSize : 100,
    color : "#FF0000"
};
ReactDOM.render(
    <h1 style = {myStyle}>文本</h1>,
    document.getElementById('app')
);
    : 注释需要写在花括号
  // {/*注释...*/}
  
  : 允许在模板中插入数组，数组会自动展开所有成员
  // var arr = [<h1>1</h1>, <h2>2<h2>,]
  // <div>{arr}</div>
```

### 条件渲染

```
[条件渲染]

	: React 中，你可以创建不同的组件来封装各种你需要的行为, 依据状态不同, 可以只渲染对应状态下的部分内容
  
  : 条件渲染和JS中的一样, 使用JS运算符if或者条件运算符去创建元素来表现当前的状态, 然后让 React 根据它们来更新 UI
  
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}

// Greeting 组件，它会根据用户是否登录来决定显示上面的哪一个组件
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
);

	: 元素变量, 使用变量来储存元素

function LoginButton(props) {
  return (
    <button onClick={props.onClick}>
      Login
    </button>
  );
}

function LogoutButton(props) {
  return (
    <button onClick={props.onClick}>
      Logout
    </button>
  );
}

// 创建一个名叫 LoginControl 的有状态的组件
// 根据当前的状态来渲染 <LoginButton /> 或者 <LogoutButton />
class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;

    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <LoginControl />,
  document.getElementById('root')
);

	: JSX 中内联条件渲染的方法
  // 与运算符 &&, 通过花括号包裹代码，你可以在 JSX 中嵌入任何表达式
  // 在 JS 中, true && expression 总是会返回 expression, 而 false && expression 总是会返回 false
  // 条件是 true，&& 右侧的元素就会被渲染，如果是 false，React 会忽略并跳过它
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);

	// 三目运算符
  
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
    </div>
  );
}

render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn ? (
        <LogoutButton onClick={this.handleLogoutClick} />
      ) : (
        <LoginButton onClick={this.handleLoginClick} />
      )}
    </div>
  );
}

	: 阻止组件渲染, render 方法直接返回 null，而不进行任何渲染
  // 组件的 render 方法中返回 null 并不会影响组件的生命周期

function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return (
    <div className="warning">
      Warning!
    </div>
  );
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    this.state = {showWarning: true};
    this.handleToggleClick = this.handleToggleClick.bind(this);
  }

  handleToggleClick() {
    this.setState(state => ({
      showWarning: !state.showWarning
    }));
  }

  render() {
    return (
      <div>
        <WarningBanner warn={this.state.showWarning} />
        <button onClick={this.handleToggleClick}>
          {this.state.showWarning ? 'Hide' : 'Show'}
        </button>
      </div>
    );
  }
}

ReactDOM.render(
  <Page />,
  document.getElementById('root')
);
```
