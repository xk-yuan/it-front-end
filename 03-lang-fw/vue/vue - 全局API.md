### Vue.extend

```
[Vue.extend]

	# {Object} options
	: 使用基础 Vue 构造器, 创建一个 "子类"
  // 参数是一个包含组件选项的对象

```

### Vue.nextTick

```
[Vue.nextTick]

	: 在下次 DOM 更新循环结束之后执行延迟回调
  // 在修改数据之后立即使用这个方法，获取更新后的 DOM

```

### Vue.set

```
[Vue.set( target, propertyName/index, value )]

	# {Object | Array} target # {string | number} propertyName/index # {any} value
	: 设置值
  // 向响应式对象中添加一个属性，并确保这个新属性同样是响应式的，且触发视图更新
  // 必须用于向响应式对象上添加新属性, 因为 Vue 无法探测普通的新增属性

```

### Vue.delete

```
[Vue.delete( target, propertyName/index )]

	# {Object | Array} target # {string | number} propertyName/index
	: 删除对象的属性
  // 对象是响应式的，确保删除能触发更新视图
  // 方法主要用于避开 Vue 不能检测到属性被删除的限制，但是你应该很少会使用它
  // 目标对象不能是一个 Vue 实例或 Vue 实例的根数据对象
```

### Vue.directive

```
[Vue.directive( id, [definition] )]

	# {string} id # {Function | Object} [definition]
	: 注册或获取全局指令
  // 自定义指令 -> https://cn.vuejs.org/v2/guide/custom-directive.html

// 注册
Vue.directive('my-directive', {
  bind: function () {},
  inserted: function () {},
  update: function () {},
  componentUpdated: function () {},
  unbind: function () {}
})

// 注册 (指令函数)
Vue.directive('my-directive', function () {
  // 这里将会被 `bind` 和 `update` 调用
})

// getter, 返回已注册的指令
var myDirective = Vue.directive('my-directive')

```

### Vue.filter

```
[Vue.filter( id, [definition] )]
	
  # {string} id | # {Function} [definition]
	: 注册或获取全局过滤器
  // 过滤器 -> https://cn.vuejs.org/v2/guide/filters.html

// 注册
Vue.filter('my-filter', function (value) {
  // 返回处理后的值
})

// getter，返回已注册的过滤器
var myFilter = Vue.filter('my-filter')
```

### Vue.component

```
[Vue.component( id, [definition] )]

	# {string} id # {Function | Object} [definition]
	: 注册或获取全局组件, 注册还会自动使用给定的id设置组件的名称
  // 组件 -> https://cn.vuejs.org/v2/guide/components.html

// 注册组件，传入一个扩展过的构造器
Vue.component('my-component', Vue.extend({ /* ... */ }))

// 注册组件，传入一个选项对象 (自动调用 Vue.extend)
Vue.component('my-component', { /* ... */ })

// 获取注册的组件 (始终返回构造器)
var MyComponent = Vue.component('my-component')

```

### Vue.use

```
[Vue.use( plugin )]

	# {Object | Function} plugin
	: 安装 Vue.js 插件
  // 插件是一个对象, 必须提供 install 方法, 插件是一个函数, 它会被作为 install 方法
  // install 方法调用时，会将 Vue 作为参数传入, 当 install 方法被同一个插件多次调用, 插件将只会被安装一次

	: 插件 -> https://cn.vuejs.org/v2/guide/plugins.html
```

### Vue.mixin

```
[Vue.mixin( mixin )]

	# {Object} mixin
	: 全局注册一个混入，影响注册之后所有创建的每个 Vue 实例
```

### Vue.compile

```
[Vue.compile( template )]

	# {string} template
	: 在 render 函数中编译模板字符串, 独立构建时有效
  // 渲染函数 -> https://cn.vuejs.org/v2/guide/render-function.html

var res = Vue.compile('<div><span>{{ msg }}</span></div>')

new Vue({
  data: {
    msg: 'hello'
  },
  render: res.render,
  staticRenderFns: res.staticRenderFns
})
```

### Vue.observable

```
[Vue.observable( object )]

	# {Object} object
	: 让一个对象可响应， Vue 内部会用它来处理 data 函数返回的对象
  // 返回的对象可以直接用于渲染函数和计算属性内, 并且会在发生改变时触发相应的更新
  // 也可以作为最小化的跨组件状态存储器, 用于简单的场景

const state = Vue.observable({ count: 0 })

const Demo = {
  render(h) {
    return h('button', {
      on: { click: () => { state.count++ }}
    }, `count is: ${state.count}`)
  }
}

```

### Vue.version

```
[Vue.version]

	: 提供字符串形式的 Vue 安装版本号
  // 这对社区的插件和组件来说非常有用, 你可以根据不同的版本号采取不同的策略

```

