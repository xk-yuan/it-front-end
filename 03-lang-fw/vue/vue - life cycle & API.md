```
---------------------------------------------------------------------------------------

[新建 Vue 实例]

[初始化 事件 & 生命周期]

	: beforeCreate

[初始化 注入 & 校验]

	: created

---------------------------------------------------------------------------------------
[初始化根元素]

	: beforeMount

[创建 vm.$el 替换 el]

	: mount

[挂载完成]
---------------------------------------------------------------------------------------

[data 相关]

	: beforeUpdate
  
  : updated

[vm.$destroy]

	: beforeDestroy
  
  : destroyed

[销毁完毕]
---------------------------------------------------------------------------------------
```

### 生命周期图

![lifecycle.png](http://localhost/it/front-end/1571497018890-717acba5-a1b3-45d5-a264-f1ab70ad8c22.png#align=left&display=inline&height=1889&name=lifecycle.png&originHeight=3039&originWidth=1200&size=77677&status=done&style=none&width=746)

### API

```
[声命周期 API]

	# Vue 实例初始化时, 声明声明周期钩子
	: https://cn.vuejs.org/v2/api/#beforeCreate







[beforeCreate]

	: 在实例初始化之后, 数据观测 (data observer) 和 event/watcher 事件配置之前被调用
  
[created]

	: 在实例创建完成后被立即调用
  // 在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。
  // 然而，挂载阶段还没开始，$el 属性目前不可见

[beforeMount]

	: 在挂载开始之前被调用, 相关的 render 函数首次被调用 (该钩子在服务器端渲染期间不被调用)

[mounted]

	: el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子
  // 如果 root 实例挂载了一个文档内元素，当 mounted 被调用时 vm.$el 也在文档内
  // mounted 不会承诺所有的子组件也都一起被挂载
  // 如果你希望等到整个视图都渲染完毕，可以用 vm.$nextTick 替换掉 mounted

mounted: function () {
  this.$nextTick(function () {
    // Code that will run only after the
    // entire view has been rendered
  })
}

[beforeUpdate]

	: 数据更新时调用，发生在虚拟 DOM 打补丁之前
  // 适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器
  // (该钩子在服务器端渲染期间不被调用，因为只有初次渲染会在服务端进行)

[updated]

	: 由于数据更改导致的虚拟 DOM 重新渲染和打补丁, 在这之后会调用该钩子 (该钩子在服务器端渲染期间不被调用)
  // 当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作
  // 然而在大多数情况下，你应该避免在此期间更改状态
  // 如果要相应状态改变，通常最好使用计算属性 (computed) 或 watcher 取而代之
  // updated 不会承诺所有的子组件也都一起被重绘
  // 如果你希望等到整个视图都重绘完毕，可以用 vm.$nextTick 替换掉 updated

updated: function () {
  this.$nextTick(function () {
    // Code that will run only after the
    // entire view has been re-rendered
  })
}

[activated]

	: keep-alive 组件激活时调用 (该钩子在服务器端渲染期间不被调用)
  // 构建组件 - keep-alive https://cn.vuejs.org/v2/api/#keep-alive
  // 动态组件 - keep-alive https://cn.vuejs.org/v2/guide/components-dynamic-async.html#%E5%9C%A8%E5%8A%A8%E6%80%81%E7%BB%84%E4%BB%B6%E4%B8%8A%E4%BD%BF%E7%94%A8-keep-alive

[deactivated]

	: keep-alive 组件停用时调用
  // 构建组件 - keep-alive https://cn.vuejs.org/v2/api/#keep-alive
  // 动态组件 - keep-alive https://cn.vuejs.org/v2/guide/components-dynamic-async.html#%E5%9C%A8%E5%8A%A8%E6%80%81%E7%BB%84%E4%BB%B6%E4%B8%8A%E4%BD%BF%E7%94%A8-keep-alive

[beforeDestroy]

	: 实例销毁之前调用 (此时, 实例仍然完全可用) (该钩子在服务器端渲染期间不被调用)

[destroyed]

	: Vue 实例销毁后调用 (该钩子在服务器端渲染期间不被调用)
  // 调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁

[errorCaptured]

	# (err: Error, vm: Component, info: string) => ?boolean
	: 当捕获一个来自子孙组件的错误时被调用 (2.5.0+ 新增)
  // 此钩子会收到三个参数：错误对象、发生错误的组件实例以及一个包含错误来源信息的字符串
  // 返回 false 以阻止该错误继续向上传播
  // 以在此钩子中修改组件的状态
  // 因此在模板或渲染函数中设置其它内容的短路条件非常重要, 防止错误被捕获时该组件进入一个无限的渲染循环
  
```

