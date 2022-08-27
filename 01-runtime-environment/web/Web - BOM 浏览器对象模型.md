
```
[官网]

	: 没有特定标准, 每个浏览器都有其对应 BOM 实现
  
  : H5 标准, 规范了BOM 标准, 使得各个浏览器之间BOM兼容

// https://www.jianshu.com/p/89edbfd637b6
// https://www.w3school.com.cn/js/js_window.asp
// https://www.cnblogs.com/lz2017/p/6792330.html
```

    浏览器对象模型 Browser Object Model BOM，用于描述这种对象与对象之间层次关系的模型，浏览器对象模型提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。

    BOM由多个对象组成，其中代表浏览器窗口的 Window对象是BOM的顶层对象，其他对象都是该对象的子对象。以window对象为依托，表示浏览器窗口和页面可见区域 ，所以 全局对象 window 是所有对象的根元素。同时window对象还是ECMAScript中的Global对象，因而所有的全局变量和函数都是它的属性和方法，且所有原声构造函数及其他函数都存在与他的命名空间下。

JavaScript的所有全局对象、全局方法和全局变量全都自动被归为window对象的方法和属性，在调用这些方法和属性的时候可以省略window。DOM也是window对象的属性。

    BOM 没有相关标准，每个浏览器都有其自己对BOM的实现方式。BOM有窗口对象、导航对象等一些实际上已经默认的标准，但对于这些对象和其它一些对象，每个浏览器都定义了自己的属性和方式。

    使用BOM可以控制浏览器显示的页面以外的部分。HTML5致力于把很多BOM功能写入正式规范。从根本上讲，BOM只处理浏览器窗口和框架，但人们习惯上也把所有针对浏览器的JavaScript扩展算作BOM的一部分。

![image.png](http://localhost/it/front-end/1572564461443-db996128-cc1d-4388-9d73-201c9e039d7b.png#align=left&display=inline&height=230&name=image.png&originHeight=160&originWidth=518&size=17206&status=done&width=746)

![image.png](http://localhost/it/front-end/1572564543064-bb89998e-9fdd-40db-a4b7-2e994c8b9312.png#align=left&display=inline&height=81&name=image.png&originHeight=126&originWidth=1166&size=28020&status=done&width=746)

### 对象层次结构

![image.png](http://localhost/it/front-end/1572565704552-be4cd87c-b7eb-460d-8c58-800c93d041e8.png#align=left&display=inline&height=419&name=image.png&originHeight=361&originWidth=643&size=79402&status=done&width=746)

```
[window]

	: 通过js访问浏览器的一个接口，又是ECMAScript规定的Global对象

  # 浏览器窗口的视窗不包括工具栏和滚动条
  : window.innerHeight # 返回浏览器窗口的高度 (像素 px)

  : window.innerWidth  # 返回浏览器窗口的宽度

[Location]

	: window.location 和 document.location引用同一个对象

[navigator]

	: 用于检测浏览器类型, 包含当前浏览器有关的信息

[screen]

	: 显示屏幕相关属性

	: width 宽 , height 高, 保存着与客户端显示器有关的信息，这些信息一般只用于站点分析

[history]

	: 不允许直接使用历史URL, 但是可以操作其前进后退

	: history.go(-1) # 回退一页
  
  : history.go(“bing.com”) # 跳转到最近的包含bing.com的页面
  
  : history.back() # 后退一页
  
  : history.forward() # 前进一页

[document]

	: 文档对象, DOM

[frames]

	# 指向当前框架对象
	: HTML自框架 , window

```

