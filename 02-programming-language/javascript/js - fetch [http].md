
![image.png](http://localhost/it/front-end/1573368213610-de09fcd4-cc6d-4c92-b7f6-4ab37a9ab98e.png)


```javascript
[]

	: https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch

	: https://www.w3cschool.cn/fetch_api/

[ployfill]

	# 第三方库, 解决浏览器不支持 Fetch 方案
	: https://github.com/github/fetch

	: https://github.com/zellwk/zl-fetch

	# 由于Fetch API是基于Promise设计，旧浏览器不支持Promise，需要使用pollyfill es6-promis
	: https://www.npmjs.com/package/es6-promise

// https://www.html.cn/archives/9907
// https://segmentfault.com/a/1190000020002674
// https://segmentfault.com/a/1190000011433064
// https://www.jianshu.com/p/8bc48f8fde75
```

    Fetch API 提供了一个 JavaScript接口，用于访问和操纵HTTP管道的部分

    其是一种HTTP数据请求的方式，是XMLHttpRequest的一种替代方案。fetch不是ajax的进一步封装，而是原生js。Fetch函数就是原生js，没有使用XMLHttpRequest对象。

    Fetch被称为下一代Ajax技术,采用Promise方式来处理数据。Fetch被称为下一代Ajax技术,采用Promise方式来处理数据。

    目前浏览器端服务器通信方式有，XMLHttpRequest(XHR)、Fetch 、jQuery实现的AJAX ，XMLHttpRequest(XHR) 和 Fetch是浏览器的原生API，jquery的ajax其实是封装了XHR。
