

```
[组件基础]

	: https://cn.vuejs.org/v2/guide/components.html
  
  -> 组件是可复用的 Vue 实例，所以组件与 Vue 实例具有相同的选项参数。
  
  -> data 必须是一个函数
  
  -> prop , 向子组件传递数据
  
  -> 自定义事件的系统 ($emit , v-on), 子组件向父组件传递事件, 传递数据
  
  -> <slot> 插槽分发内容
  
  -> is 属性, 动态组件 # <component v-bind:is="currentTabComponent"></component>

	# 组件名

[组件注册]

	: 全局组件注册 => Vue.component
  
  : 局部组件注册 => components 属性参数
  # 局部注册的组件在其子组件中不可用
  
  : 模块系统

[单文件组件]

	: 文件扩展名为 .vue 的 single-file components(单文件组件)

// https://cn.vuejs.org/v2/guide/components-registration.html
```

```
[组件]

	: 组件可以扩展 HTML 元素，封装可重用的代码。

[注册 - 全局组件]

	: Vue.component(componentname, options)
  # 组件名
	# 配置选项

[调用]

	: <componentname></componentname>

[组测 - 局部组件]

# 定义组件模板
var Child = {
    template: '<h1>自定义组件!</h1>'
}

# 实例化 Vue时注册
components: {
    // <componentname> 将只在父模板可用
    'componentname': Child
}

	: 使用 <componentname></componentname>
  # 只能在模板中可用


[组件数据传递 - Prop]

	: 父组件通过属性, props 将数据传递给子组件
	# 子组件需要显式地用 props 选项声明 "prop"

	: 动态 Prop
  
  : Prop 验证

[组件数据传递 - 自定义事件]

	: 子组件通过自定义事件, 将数据从子组件传递给父组件

	:  v-on 绑定自定义事件, 每个 Vue 实例都实现了事件接口(Events interface)
  # $on(eventName) 监听事件
  # $emit(eventName) 触发事件

	: 父组件可以在使用子组件的地方直接用 v-on 来监听子组件触发的事件

```
