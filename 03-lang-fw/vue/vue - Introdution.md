
```
[官网]

	: https://cn.vuejs.org/

	: https://github.com/vuejs/vue

[api]

	: https://cn.vuejs.org/v2/api/

[文档]

	: https://cn.vuejs.org/v2/guide/

  : https://cn.vuejs.org/v2/cookbook

  : https://learning.dcloud.io/#/?vid=1
  
  : https://vuex.vuejs.org/zh/

[视频]

	: https://learning.dcloud.io/#/?vid=0

// http://xiaolongwu.cn/
```

> [《Vue.js 权威指南 张耀春 201609.pdf》]()

> [《Vue.js 项目开发实战 张帆 201808.pdf》]()

    Vue 被设计为可以自底向上逐层应用，Vue 的核心库只关注视图层。核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统。

    其核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统。

```
[数据和方法]

[生命周期]

[模板语法-插值]

[模板语法-指令]

[class-style 绑定]

[条件渲染]

[列表渲染]

[事件绑定]

[表单输入绑定]

```

```
[文件]

	: VUE.JS # 用户界面JS框架 # 安装 [文件安装、nodejs安装]

[内容模块]

	: 数据

  : 方法
  
  : 生命周期 [Vue组件]

  : CSS 渲染 - [class 和 style 样式控制] 
  # 属性样式
  # v-bind -> v-bind:class 、 :class -> v-bind:style 、:style

[Vue 实例化属性]

	: el # 选定元素
  
  : data # 数据
  
  : methods # 方法

  : computed # 计算属性 (get/set) // 响应式依赖进行缓存

	: watch # 侦听属性、侦听器

[语法]

	: [模板语法-插值、模板语法-指令]

[指令]

	: 条件渲染
  # v-if v-else  v-else-if  // 更高的切换开销
  # 管理可复用的元素 -> key
  # v-show // 更高的初始渲染开销

  : 列表渲染
  # v-for 基于一个数组来渲染一个列表

  : 事件监听
  # v-on

  : 表单输入绑定 - 双向数据绑定 - 事件绑定 [modle-view 单向绑定、双向绑定]
  # v-model

[组件 [基础、注册、单文件]]

	: props
  # 子组件传递数据
  
  : template


```

### 模板语法

```
[模板语法]

	: 基于 HTML 的模板语法, 允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据
  // 模板都是合法的 HTML ，所以能被遵循规范的浏览器和 HTML 解析器解析
	// 底层的实现上，Vue 将模板编译成虚拟 DOM 渲染函数
  // 结合响应系统，Vue 能够智能地计算出最少需要重新渲染多少组件，并把 DOM 操作次数减到最少

[渲染函数 & JSX]

```

```
[模版语法]

	: 基于 HTML 的模版语法, 允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据
	: Vue其核心是一个允许你采用简洁的模板语法来声明式的将数据渲染进 DOM 的系统
  ：结合响应系统, 数据状态改变时, 能够重新计算并渲染组件到 DOM 操作上

[01 数据绑定 - 插值 {{html 文本}}]

	: {{}}
  # <p>{{ message }}</p>
  
  :  v-html 指令用于输出 html 代码
  # <p v-html='message'></p>


[过滤器]

	: {{ message | capitalize }}<div v-bind:id="rawId | formatId"></div>
			filters: {
            // 对输入的字符串第一个字母转为大写
            capitalize: function (value) {
                if (!value) return ''
                value = value.toString()
                return value.charAt(0).toUpperCase() + value.slice(1)
            }
        }

	# 文本格式化, "管道符"指示
  # 过滤器函数接受表达式的值作为第一个参数




```

### 表达式

```
[表达式]

	: {{5+5}}
  : {{ ok ? 'YES' : 'NO' }}
  : {{ message.split('').reverse().join('') }}

```

### 指令 [v-if v-for v-show]

```
[指令]

	: 带 v- 前缀的特殊属性, 指令用于在表达式的值改变时，将某些行为应用到 DOM 上

	:  v-if 指令 -> 根据表达式 seen 的值(true 或 false )来决定是否插入 p 元素
  # <p v-if="seen">Seen</p>
  # data.seen = false

[参数]

	: 参数在指令后以冒号指明 -> v-bind:herf="url"
  # v-bind 指令被用来响应地更新 HTML 属性
  # href 是参数，告知 v-bind 指令将该元素的 href 属性与表达式 url 的值绑定
  
  # v-on:click="doSomething"
  # 监听事件

[条件语句]

	: v-if  | v-else | v-else-if

// seen 确认是否插入p元素
<p v-if="seen">现在你看到我了</p>

// 字符串模板
{{#if ok}}
  <h1>Yes</h1>
{{/if}}

	: v-show # 根据条件展示元素, 与v-if区别为, 已经渲染到缓存, 只是class属性进行隐藏

[循环语句]

	: v-for
  #  site in sites 形式的特殊语法， sites 是源数据数组并且 site 是数组元素迭代的别名
  
  # v-for="site in sites" -> {{ site.name }}
  
  # 迭代对象
  # v-for="value in object" -> {{ value }}
  # v-for="(value, key) in object" -> {{ key }} : {{ value }}
  # v-for="(value, key, index) in object" ->  {{ index }}. {{ key }} : {{ value }}
  # v-for="n in 10" -> {{ n }}

```

```
[事件处理器]

	: v-on

	<p style = "font-size:25px;">{{ counter }}</p>
  <button @click = "counter++" style = "font-size:25px;">click</button>

[事件修饰符]

	: 修饰符是以半角句号 . 指明的特殊后缀, 用于指出一个指令应该以特殊方式绑定
  
  : .prevent 修饰符告诉 v-on 指令对于触发的事件调用 event.preventDefault()
  # <form v-on:submit.prevent="onSubmit"></form>

<!-- 阻止单击事件冒泡 -->
<a v-on:click.stop="doThis"></a>
<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>
<!-- 修饰符可以串联  -->
<a v-on:click.stop.prevent="doThat"></a>
<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>
<!-- 添加事件侦听器时使用事件捕获模式 -->
<div v-on:click.capture="doThis">...</div>
<!-- 只当事件在该元素本身（而不是子元素）触发时触发回调 -->
<div v-on:click.self="doThat">...</div>

<!-- click 事件只能点击一次，2.1.4版本新增 -->
<a v-on:click.once="doThis"></a>

  按键修饰符

<!-- 只有在 keyCode 是 13 时调用 vm.submit() -->
<input v-on:keyup.13="submit">
<!-- 同上 -->
<input v-on:keyup.enter="submit">
<!-- 缩写语法 -->
<input @keyup.enter="submit">
// .enter  .tab  .delete (捕获 "删除" 和 "退格" 键) .esc .space .up .down .left
// .right  .ctrl  .alt  .shift  .meta

[缩写]

	: v-bind -> :

  : v-on -> @

[自定义指令]

// 自动获取焦点
<input v-focus>

// 注册一个全局自定义指令 v-focus
Vue.directive('focus', {
  // 当绑定元素插入到 DOM 中。
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})

// 属性注册
directives: {
  // 注册一个局部的自定义指令 v-focus
  focus: {
    // 指令的定义
    inserted: function (el) {
      // 聚焦元素
      el.focus()
    }
  }
}

[函数钩子]

	: bind -> 只调用一次, 指令第一次绑定到元素时调用
  # 用这个钩子函数可以定义一个在绑定时执行一次的初始化动作

	: inserted -> 被绑定元素插入父节点时调用 (父节点存在即可调用, 不必存在于 document 中)

	: update -> 被绑定元素所在的模板更新时调用, 而不论绑定值是否变化
  # 通过比较更新前后的绑定值, 可以忽略不必要的模板更新

	: componentUpdated -> 被绑定元素所在模板完成一次更新周期时调用

	: unbind -> 只调用一次, 指令与元素解绑时调用

-> 参数

	: el -> 指令所绑定的元素, 可以用来直接操作 DOM

	: binding -> 一个对象，包含以下属性
	# name  -> 指令名, 不包括 v- 前缀
	# value -> 指令的绑定值
	# oldValue -> 指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用
	# expression: 绑定值的表达式或变量名
	# arg: 传给指令的参数。例如 v-my-directive:foo， arg 的值是 "foo"。
	# modifiers: 一个包含修饰符的对象
	# vnode: Vue 编译生成的虚拟节点
	# oldVnode: 上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用

<div id="app"  v-runoob:hello.a.b="message">

Vue.directive('runoob', {
  bind: function (el, binding, vnode) {
    var s = JSON.stringify
    el.innerHTML =
      'name: '       + s(binding.name) + '<br>' +
      'value: '      + s(binding.value) + '<br>' +
      'expression: ' + s(binding.expression) + '<br>' +
      'argument: '   + s(binding.arg) + '<br>' +
      'modifiers: '  + s(binding.modifiers) + '<br>' +
      'vnode keys: ' + Object.keys(vnode).join(', ')
  }
})

Vue.directive('runoob', function (el, binding) {
  // 设置指令的背景颜色
  el.style.backgroundColor = binding.value.color
})
```

### 样式绑定 - class style

```
[样式绑定]

	: HTML 元素的属性 -> class style -> 设置元素的样式
  
  : v-bind 来设置样式属性
  # 表达式的结果类型除了字符串之外, 还可以是对象或数组

[class 属性绑定]

	: v-bind:class 设置一个对象，从而动态的切换 class
  
  #
  : data.isActive = false

	# HTML
	: <input type="checkbox" v-model="isActive"/>
  : <p v-bind:class="{ active-calss: isActive }"></p>

  : <p v-bind:class="{ active-calss: isActive , active-calss1: isActive1}"></p>
  <p v-bind:class="[active-calss, active-calss1]"></p> #数组
  <p v-bind:style="{ color: active-calss-color, fontSize: fontSize + 'px' }"></p>
  # 样式
  <style>
		p.active-calss{color:red; font-size:50px}
	</style>

```

-----------------------------------------------------------------------------------------------------------------------
### v-model - 输入数据与双向绑定

![](../../imgs/1571802074643-2a370381-905f-4c63-b359-826cc8d873d0.png#align=left&display=inline&height=396&originHeight=372&originWidth=700&size=0&status=done&style=none&width=746)

```
[用户输入]

	: v-model 指令来实现双向数据绑定
  # <p>{{ message }}</p><input v-model="message">
  # data.message = 'hello'

  : v-model 指令用来在 input、select、textarea、checkbox、radio 等表单控件元素上创建
  双向数据绑定, 根据表单上的值, 自动更新绑定的元素的值

[表单 - 输入框]

<input v-model="message" placeholder="edit ...">
<p>{{ message }}</p>

<textarea v-model="message2" placeholder="edit ..."></textarea>
<p style="white-space: pre">{{ message2 }}</p>

[表单 - 复选框]

	: checked : false,checkedNames: []

<p>单个复选框</p>
<input type="checkbox" id="checkbox" v-model="checked">
<label for="checkbox">{{ checked }}</label>

<p>多个复选框</p>
<input type="checkbox" id="runoob" value="Runoob" v-model="checkedNames">
<label for="runoob">A</label>
<input type="checkbox" id="google" value="Google" v-model="checkedNames">
<label for="google">B</label>
<br>
<span>选择的值为: {{ checkedNames }}</span>

[表单 - 单选按钮]

	: data.picked = "AD"

<input type="radio" id="a" value="AD" v-model="picked">
<label for="a">A</label>
<br>
<input type="radio" id="b" value="BD" v-model="picked">
<label for="b">B</label>
<br>
<span>{{ picked }}</span>

[表单 - select 列表]

	: data.selected = ""

<select v-model="selected" name="fruit">
  <option value="">请选择</option>
  <option value="www.A.com">A</option>
  <option value="www.B.com">B</option>
</select>
<br/>
<p>{{selected}}</p>

[修饰符]

	: v-model.lazy
  # 在默认情况下, v-model 在 input 事件中同步输入框的值与数据, lazy 变为在 change 事件中同步
  # 在 "change" 而不是 "input" 事件中更新

	: v-model.number
  # 自动将用户的输入值转为 Number 类型（如果原值的转换结果为 NaN 则返回原值）
  # <input v-model.number="age" type="number">
  
  : v-model.trim
  # 自动过滤用户输入的首尾空格

```
