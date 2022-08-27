# Vue Use

> [Vue.js 使用案例](https://v3.cn.vuejs.org/guide/introduction.html#声明式渲染)

- 声明式渲染
- 处理用户输入
- 条件与循环
- 组件化应用构建

## 声明式渲染

Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统。数据和 DOM 已经被建立了关联，所有东西都是响应式的。


```js Vue.js
<div id="counter">
  Counter: {{ counter }}
</div>


const Counter = {
  data() {
    return {
      counter: 0
    }
  }
}

Vue.createApp(Counter).mount('#counter')
```

```js
// counter property 每秒递增，你将看到渲染的 DOM 是如何变
const Counter = {
  data() {
    return {
      counter: 0
    }
  },
  mounted() {
    setInterval(() => {
      this.counter++
    }, 1000)
  }
}
```

除了文本插值，我们还可以像这样绑定元素的 attribute

```js Vue.js
// v-bind attribute 被称为指令。指令带有前缀 v-，以表示它们是 Vue 提供的特殊 attribute。它们会在渲染的 DOM 上应用特殊的响应式行为。
// 将这个元素节点的 title attribute 和当前活跃实例的 message property 保持一致
<div id="bind-attribute">
  <span v-bind:title="message">
    鼠标悬停几秒钟查看此处动态绑定的提示信息！
  </span>
</div>

const AttributeBinding = {
  data() {
    return {
      message: 'You loaded this page on ' + new Date().toLocaleString()
    }
  }
}

Vue.createApp(AttributeBinding).mount('#bind-attribute')
```

## 处理用户输入

```js Vue.js
// 为了让用户和应用进行交互，我们可以用 v-on 指令添加一个事件监听器，通过它调用在实例中定义的方法：
<div id="event-handling">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">反转 Message</button>
</div>

const EventHandling = {
  data() {
    return {
      message: 'Hello Vue.js!'
    }
  },
  methods: {
    reverseMessage() {
      this.message = this.message
        .split('')
        .reverse()
        .join('')
    }
  }
}

Vue.createApp(EventHandling).mount('#event-handling')
```

## 
