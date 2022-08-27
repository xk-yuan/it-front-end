# web components

> 模块化, 自定义标签技术

> Web components 的一个重要属性是封装——可以将标记结构、样式和行为隐藏起来，并与页面上的其他代码相隔离，保证不同的部分不会混在一起，可使代码更加干净、整洁。

> Shadow DOM 接口是关键所在，它可以将一个隐藏的、独立的 DOM 附加到一个元素上。


## 资源

> [Web Components - 自定义标签](https://developer.mozilla.org/zh-CN/docs/Web/Web_Components)
>
>   - [web-components-examples](https://github.com/mdn/web-components-examples.git)

> [<template> 内容模板元素](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/template)
>
> [<slot> 占位符](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/slot)
>
> [Using templates and slots](https://developer.mozilla.org/zh-CN/docs/Web/Web_Components/Using_templates_and_slots)


> [CustomElementRegistry 包含自定义元素相关功能](https://developer.mozilla.org/zh-CN/docs/Web/API/CustomElementRegistry)
>
>   - [CustomElementRegistry.define() 注册新的自定义元素](https://developer.mozilla.org/zh-CN/docs/Web/API/CustomElementRegistry/define)
>
>   - [Window.customElements 返回 CustomElementRegistry 对象的引用](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/customElements)
>
> [Element.attachShadow()](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/attachShadow)
>
> [Using_custom_elements](https://developer.mozilla.org/zh-CN/docs/Web/Web_Components/Using_custom_elements)


> [ShadowRoot](https://developer.mozilla.org/zh-CN/docs/Web/API/ShadowRoot)
>
>  - [Element.attachShadow() 将shadow DOM树附加给特定元素](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/attachShadow)
>
>  - [Element.shadowRoot 返回附加给特定元素的shadow root](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/shadowRoot)
>
> [Using shadow DOM](https://developer.mozilla.org/zh-CN/docs/Web/Web_Components/Using_shadow_DOM)


> [Web Components 入门实例教程](https://www.ruanyifeng.com/blog/2019/08/web_components.html)
>
> [Web Components使用（一）](https://blog.csdn.net/iotzzh/article/details/108766578)
>
> [Web Components简介](https://www.jianshu.com/p/a74db98cb2f3)


## 简介

Web Components 是一套不同的技术，允许您创建可重用的定制元素（它们的功能封装在您的代码之外）并且在您的web应用中使用它们。

> 依赖技术
>
> - a. Custom elements（自定义元素）  一组JavaScript API，允许您定义custom elements及其行为，然后可以在您的用户界面中按照需要使用它们。
>
> - b. Shadow DOM（影子DOM）         一组JavaScript API，用于将封装的“影子”DOM树附加到元素（与主文档DOM分开呈现）并控制其关联的功能。
>
> - c. HTML templates（HTML模板）   <template> 和 <slot> 元素使您可以编写不在呈现页面中显示的标记模板。然后它们可以作为自定义元素结构的基础被多次重用。

> 使用步骤
>
> 1. 创建一个类或函数来指定web组件的功能，如果使用类，请使用 ECMAScript 2015 的类语法(参阅类获取更多信息)。
>
> 2. 使用 CustomElementRegistry.define() 方法注册您的新自定义元素，并向其传递要定义的元素名称、指定元素功能的类、以及可选的其所继承自的元素。
>
> 3. 可以, 使用Element.attachShadow() 方法将一个shadow DOM附加到自定义元素上, 使用通常的DOM方法向shadow DOM中添加子元素、事件监听器等等。
>
> 4. 可以, 使用 <template> 和 <slot> 定义一个HTML模板。再次使用常规DOM方法克隆模板并将其附加到您的shadow DOM中。
>
> 5. 在页面任何您喜欢的位置使用自定义元素，就像使用常规HTML元素那样。

> 自定义元素生命周期函数 [](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements#using_the_lifecycle_callbacks)
>
> 1. connectedCallback: 当自定义元素第一次被连接到文档DOM时被调用
>
> 2. disconnectedCallback: 当自定义元素与文档DOM断开连接时被调用
>
> 3. adoptedCallback: 当自定义元素被移动到新文档时被调用
>
> 4. attributeChangedCallback: 当自定义元素的一个属性被增加、移除或更改时被调用


### <template> 内容模板元素

一种用于保存客户端内容机制，该内容在加载页面时不会呈现，但随后可以(原文为 may be)在运行时使用JavaScript实例化。

将模板视为一个可存储在文档中以便后续使用的内容片段。虽然解析器在加载页面时确实会处理<template>元素的内容，但这样做只是为了确保这些内容有效；但元素内容不会被渲染。

> solt 占位符
>
> - name  属性, 插槽的名字, 拥有name属性的插槽叫具名插槽

Web组件内的一个占位符。该占位符可以在后期使用自己的标记语言填充，这样您就可以创建单独的DOM树，并将它与其它的组件组合在一起。


#### example

```html
<table id="producttable">
  <thead>
    <tr>
      <td>UPC_Code</td>
      <td>Product_Name</td>
    </tr>
  </thead>
  <tbody>
    <!-- 现有数据可以可选地包括在这里 -->
  </tbody>
</table>

<template id="productrow">
  <tr>
    <td class="record"></td>
    <td></td>
  </tr>
</template>

<script>
    // 通过检查来测试浏览器是否支持HTML模板元素
    // 用于保存模板元素的内容属性。
    if ('content' in document.createElement('template')) {
        // 使用现有的HTML tbody实例化表和该行与模板
        let t = document.querySelector('#productrow'),
        td = t.content.querySelectorAll("td");
        td[0].textContent = "1235646565";
        td[1].textContent = "Stuff";

        // 克隆新行并将其插入表中
        let tb = document.getElementsByTagName("tbody");
        let clone = document.importNode(t.content, true);
        tb[0].appendChild(clone);

        // 创建一个新行
        td[0].textContent = "0384928528";
        td[1].textContent = "Acme Kidney Beans";

        // 克隆新行并将其插入表中
        let clone2 = document.importNode(t.content, true);
        tb[0].appendChild(clone2);

        } else {
        // 找到另一种方法来添加行到表，因为不支持HTML模板元素。
        }
  }
</script>
```

```html template
<!--
  此模板代码, 不会再页面显示, 直到使用 JavaScript获取并引用添加到DOM中, 才会渲染显示
-->
<template id="my-paragraph">
  <p>My paragraph</p>
</template>

<!--
  引用模板代码, 插入到DOM中
-->
<script>
  let template = document.getElementById('my-paragraph');
  let templateContent = template.content;
  document.body.appendChild(templateContent);
</script>

<!--
  添加<style>样式标签
-->
<template id="my-paragraph">
  <style>
    p {
      color: white;
      background-color: #666;
      padding: 5px;
    }
  </style>
  <p>My paragraph</p>
</template>

<!-- 添加slot插槽 -->
<template id="my-paragraph">
  <p>My paragraph</p>
  <p><slot name="my-text">My default text</slot></p>
</template>

<!-- 使用 -->
<my-paragraph>
  <span slot="my-text">Let's have some different text!</span>
</my-paragraph>

<my-paragraph>
  <ul slot="my-text">
    <li>Let's have some different text!</li>
    <li>In a list!</li>
  </ul>
</my-paragraph>
```

```html 自定义tag模板
<!--
  定义一个模板组件, <my-paragraph>

  模板（模板）制作就是细节，而与网络组件（网络组件）一起使用效果更好。
-->

<script>
  customElements.define('my-paragraph',
    class extends HTMLElement {
      constructor() {
        super();
        let template = document.getElementById('my-paragraph');
        let templateContent = template.content;

        // 使用Node.cloneNode()方法添加了模板的拷贝到底部的根结点上
        const shadowRoot = this.attachShadow({mode: 'open'})
          .appendChild(templateContent.cloneNode(true));
    }
})
</script>

<!-- 使用注册的模板标签 -->
<my-paragraph></my-paragraph>
```
