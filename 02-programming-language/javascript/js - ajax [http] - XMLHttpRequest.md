
```
[]

	: https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest

	: https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX

	: https://api.jquery.com/category/ajax/

// https://www.w3school.com.cn/ajax/index.asp
// https://www.runoob.com/ajax/ajax-tutorial.html
```

    Asynchronous Javascript And XML, Asynchronous Javascript And XML , Ajax ，一种创建交互式网页应用的网页开发技术。

    一种用于，在无需重新加载整个网页的情况下，能够更新部分网页，创建快速动态网页的技术。通过在后台与服务器进行少量数据交换，Ajax 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

    Ajax 不是一种新的编程语言，而是一种用于创建更好更快以及交互性更强的Web应用程序的技术，一种独立于 Web 服务器软件的浏览器技术。

    该技术在 1998 年前后得到了应用。允许客户端脚本发送HTTP请求（XMLHTTP）的第一个组件由Outlook Web Access小组写成。Ajax 这个词由《Ajax: A New Approach to Web Applications》一文所创，该文的迅速传播加强了人们使用该项技术的意识。

    使用 用户核心对象XMLHttpRequest 向服务器提出请求并处理响应而不阻塞。可在不重载页面的情况与 Web 服务器交换数据。

    简单的说，AJAX就是在Javascript中多添加了一个对象，XMLHttpRequest对象。所有的异步交互都是使用XMLHttpRequest对象完成的。当然，各个浏览器对XMLHttpRequest的支持也是不同的

```javascript
[创建对象 XMLHttpRequest]

一般浏览器版本 -> var xmlHttp = new XMLHttpRequest()
IE5.5及更早版本, -> var xmlHttp = new ActiveXObject(“Microsoft.XMLHTTP”)
IE6 版本 -> var xmlHttp = new ActiveXObject(“Msmxl2.XMLHTTP”)

[Create XMLHttpRequest Object]

// 创建XMLHttpRequest Object
function createXMLHttpRequest() {
  var xmlHttp;
  // 适用于大多数浏览器, 以及IE7和IE更高版本
  try {
    xmlHttp = new XMLHttpRequest();
  } catch (e) {
    // 适用于IE6
    try {
      xmlHttp = new ActiveXObject("Msxml2.XMLHTTP");
    } catch (e) {
      // 适用于IE5.5, 以及IE更早版本
      try {
        xmlHttp = new ActiveXObject("Microsoft.XMLHTTP");
      } catch (e) {}
    }
  }
  return xmlHttp;
}
```

