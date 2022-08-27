# global attributes

> 全局属性

## 资源

> [Global attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes)


## 简介

所有 HTML 元素共有的属性；它们可以用于所有元素，尽管它们可能对某些元素没有影响。


### 全局属性

1. class

以空格分隔的元素类列表。类允许 CSS 和 JavaScript 通过类选择器或方法（如方法）选择和访问特定元素 Document.getElementsByClassName()。

[Document.getElementsByClassName()](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)

2. data-*

形成一类称为自定义数据属性的属性，允许在HTML及其DOM表示之间交换可由脚本使用的专有信息。

所有这些自定义数据都可以通过HTMLElement设置属性的元素的接口获得。该[HTMLElement.dataset](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dataset)属性允许访问它们。

3. hidden

Boolean 属性表示该元素尚未或不再相关。例如，它可用于隐藏在登录过程完成之前无法使用的页面元素。浏览器不会呈现此类元素。此属性不得用于隐藏可以合法显示的内容。

4. id

定义在整个文档中必须是唯一的唯一标识符 (ID)。它的目的是在链接（使用片段标识符）、脚本或样式（使用 CSS）时识别元素。

5. nonce

一个加密随机数（“使用一次的数字”），内容安全策略可以使用它来确定是否允许继续进行给定的提取。

6. part

元素的部分名称的空格分隔列表。部件名称允许 CSS 通过::part伪元素选择阴影树中的特定元素并为其设置样式。

7. sort

将shadow DOM阴影树中slot的插槽分配给元素：具有属性的元素被分配给<slot>由其name属性值与该slot属性值匹配的元素创建的插槽。

8. style

包含要应用于元素的CSS样式声明。请注意，建议在单独的一个或多个文件中定义样式。此属性和<style>元素的主要目的是允许快速设置样式，例如用于测试目的。

9. title

包含表示与其所属元素相关的咨询信息的文本。这样的信息通常可以但不一定作为工具提示呈现给用户。

