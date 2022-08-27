### 数据 [data & props]

```
[data]

[props]

// https://cn.vuejs.org/v2/api/#%E9%80%89%E9%A1%B9-%E6%95%B0%E6%8D%AE
```

### computed 计算属性

```
[computed]

	# { [key: string]: Function | { get: Function, set: Function } }
	: 计算属性将被混入到 Vue 实例中, 所有 getter 和 setter 的 this 上下文自动地绑定为 Vue 实例
  // 如果你为一个计算属性使用了箭头函数，则 this 不会指向这个组件的实例
  // 仍然可以将其实例作为函数的第一个参数来访问

	: 计算属性的结果会被缓存，除非依赖的响应式属性变化才会重新计算
  // 如果某个依赖 (比如非响应式属性) 在该实例范畴之外，则计算属性是不会被更新的

var vm = new Vue({
  data: { a: 1 },
  computed: {
    // 仅读取
    aDouble: function () {
      return this.a * 2
    },
    // 读取和设置
    aPlus: {
      get: function () {
        return this.a + 1
      },
      set: function (v) {
        this.a = v - 1
      }
    }
  }
})

[计算属性 - computed 处理复杂逻辑]

	# 反转字符串表达式
	: {{ message.split('').reverse().join('') }}
  
  #  <p>{{ message }}</p><p>{{ reversedMessage }}</p>
  data: { message:"xxx"},
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
  // 提供的函数将用作属性 vm.reversedMessage 的 getter
	// vm.reversedMessage 依赖于 vm.message, 
  // 在 vm.message 发生改变时，vm.reversedMessage 也会更新
  
  # computed 属性默认只有 getter ，不过在需要时你也可以提供一个 setter 
  computed: {
    reversedMessage: {
      // getter
      get: function () {
        return ' '
      },
      // setter
      set: function (newValue) {
      }
    }
	}

[computed vs methods]

	: methods 来替代 computed, 效果上两个都是一样的
  : 但是 computed 是基于它的依赖缓存,
  : 只有相关依赖发生改变时才会重新取值, 而使用 methods, 在重新渲染的时候,函数总会重新调用执行
  : 使用 computed 性能会更好，但是如果你不希望缓存，你可以使用 methods 属性

```

### methods

```
[methods]

	# { [key: string]: Function }
	: 将被混入到 Vue 实例中, 可以直接通过 VM 实例访问这些方法, 或者在指令表达式中使用
  // 方法中的 this 自动绑定为 Vue 实例
  // (不应该使用箭头函数来定义 method 函数, 箭头函数绑定了父级作用域的上下文)

var vm = new Vue({
  data: { a: 1 },
  methods: {
    plus: function () {
      this.a++
    }
  }
})
```

### watch 监听属性

```
[watch]

	# { [key: string]: string | Function | Object | Array }
	: 一个对象, 键是需要观察的表达式, 值是对应回调函数 (值也可以是方法名, 或者包含选项的对)
  // Vue 实例将会在实例化时调用 $watch(), 遍历 watch 对象的每一个属性

var vm = new Vue({
  data: {
    a: 1,
    b: 2,
    c: 3,
    d: 4,
    e: {
      f: {
        g: 5
      }
    }
  },
  watch: {
    a: function (val, oldVal) {
      console.log('new: %s, old: %s', val, oldVal)
    },
    // 方法名
    b: 'someMethod',
    // 该回调会在任何被侦听的对象的 property 改变时被调用, 不论其被嵌套多深
    c: {
      handler: function (val, oldVal) { /* ... */ },
      deep: true
    },
    // 该回调将会在侦听开始之后被立即调用
    d: {
      handler: 'someMethod',
      immediate: true
    },
    e: [
      'handle1',
      function handle2 (val, oldVal) { /* ... */ },
      {
        handler: function handle3 (val, oldVal) { /* ... */ },
        /* ... */
      }
    ],
    // watch vm.e.f's value: {g: 5}
    'e.f': function (val, oldVal) { /* ... */ }
  }
})
vm.a = 2 // => new: 2, old: 1

[监听属性 - watch]

	: 响应数据的变化
  <p style = "font-size:25px;">{{ counter }}</p>
  <button @click = "counter++" style = "font-size:25px;">click</button>
  
  data.counter = 1
  
  // 添加属性监听器, 值变化时调用 | nval 原始值, oval 结果值
  vm.$watch('counter', function(nval, oval) {
        //
        alert('计数器值的变化 :' + oval + ' 变为 ' + nval + '!');
  });
```

