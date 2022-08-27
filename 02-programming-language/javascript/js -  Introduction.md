![image.png](../../imgs/1572484922874-834d5f2f-1e71-4b3a-a8d5-f8009f280106.png#align=left&display=inline&height=148&margin=%5Bobject%20Object%5D&name=image.png&originHeight=201&originWidth=1015&size=57556&status=done&style=none&width=746)


```
[官网]

	: https://www.javascript.com/

[JS 引擎]

	: js 语言编译器, 存在于浏览器中, 例如 V8 引擎 , WebKit

[参考文档]

	# 基础
  : https://wangdoc.com/javascript/ | http://javascript.ruanyifeng.com/#introduction
  # https://github.com/ruanyf/jstutorial
  
  # 进阶
  : http://es6.ruanyifeng.com/
 
##
// https://www.w3school.com.cn/js/index.asp
// https://www.liaoxuefeng.com/
// https://www.liaoxuefeng.com/wiki/1022910821149312
// http://caibaojian.com/t/javascript
// https://www.cnblogs.com/lhb25/category/146074.html
```


[JavaScript 高级程序设计 第三版 李松峰 201203.pdf]()


[JavaScript 开发框架权威指南 一心一译 201705.pdf]()


[学习 JavaScript 数据结构与算法 第二版 邓钢 201709.pdf]()


    解释性, 直译式脚本语言，是一种动态类型、弱类型、基于原型的语言，内置支持类型。JavaScript 兼容于ECMA标准，因此也称为ECMAScript。

    JavaScript 是一种轻量级的脚本语言。所谓“脚本语言”，指的是它不具备开发操作系统的能力，而是只用来编写控制其他大型应用程序的“脚本”。

    JavaScript 是一种嵌入式（embedded）语言。它本身提供的核心语法不算很多，只能用来做一些数学和逻辑运算。JavaScript 本身不提供任何与 I/O（输入/输出）相关的 API，都要靠宿主环境（host）提供，所以 JavaScript 只合适嵌入更大型的应用程序环境，去调用宿主环境提供的底层 API。


    1995年时，由Netscape公司的Brendan Eich，在网景导航者浏览器上首次设计实现而成。


    解释器被称为JavaScript引擎，为浏览器的一部分，广泛用于客户端的脚本语言，最早是在HTML（标准通用标记语言下的一个应用）网页上使用，用来给HTML网页增加动态功能。


    为了让JavaScript成为全球标准，几个公司联合ECMA（European Computer Manufacturers Association）组织定制了JavaScript语言的标准，被称为ECMAScript标准。


    ECMAScript ，描述了该语javascript组成javascript组成言的语法和基本对象。还包含，文档对象模型（DOM），描述处理网页内容的方法和接口，浏览器对象模型（BOM），描述与浏览器进行交互的方法和接口。


    简单说来就是，ECMAScript是一种语言标准，而JavaScript是网景公司对ECMAScript标准的一种实现。


    谷歌V8引擎浏览器端，为JavaScript语言提供了运行环境，而NODEJS等项目，通过封装V8引擎在服务端提供JS的运行环境。


### 组成部分 - 浏览器端(H5端)


![](../../imgs/1572484118452-b87d5ede-6a1e-4e76-83e9-67707c377507.gif#align=left&display=inline&height=316&margin=%5Bobject%20Object%5D&originHeight=106&originWidth=250&size=0&status=done&style=none&width=746)


```
[组成部分 - 浏览器端]

  : 标准 - ECMAScript，描述了该语言的语法和基本对象

  : DOM - 文档对象模型, 描述处理网页内容的方法和接口

  : BOM - 浏览器对象模型, 描述与浏览器进行交互的方法和接口

[基本数据类型、表达式、算术运算符、程序的基本程序框架]

  : 四种基本的数据类型和两种特殊数据类型用来处理数据和文字
```


### 历史版本


    JavaScript已经被Netscape公司提交给ECMA制定为标准，称之为ECMAScript，标准编号ECMA-262。


  最初由Netscape的Brendan Eich设计。JavaScript是甲骨文公司的注册商标。Ecma国际以JavaScript为基础制定了ECMAScript标准。Netscape在最初将其脚本语言命名为LiveScript，后来Netscape在与Sun合作之后将其改名为JavaScript。


  JavaScript最初受Java启发而开始设计的，目的之一就是“看上去像Java”，因此语法上有类似之处，一些名称和命名规范也借自Java。但JavaScript的主要设计原则源自Self和Scheme。发展初期，JavaScript的标准并未确定，同期有Netscape的JavaScript，微软的JScript和CEnvi的ScriptEase三足鼎立。1997年，在ECMA（欧洲计算机制造商协会）的协调下，由Netscape、Sun、微软、Borland组成的工作组确定统一标准：ECMA-262。

| 版本 | 发布日期 | 基于 | Netscape Navigator | Mozilla Firefox | Internet Explorer | Opera | Safari | Google Chrome |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1.0 | 1996年3月 |  | 2.0 |  |  |  |  |  |
| 1.1 | 1996年8月 |  | 3.0 |  | 3.0 |  |  |  |
| 1.2 | 1997年6月 |  | 4.0-4.05 |  |  |  |  |  |
| 1.3 | 1998年10月 | ECMA-262 1 edition / ECMA-262 2 edition | 4.06-4.7x |  | 4.0 |  |  |  |
| 1.4 |  |  | Netscape
　　Server |  |  |  |  |  |
| 1.5 | 2000年11月 | ECMA-262 3 edition | 6.0 | 1.0 | 5.5 (JScript 5.5),
　　6 (JScript 5.6),
　　7 (JScript 5.7),
　　8 (JScript 6) | 6.0,
　　7.0,
　　8.0,
　　9.0 |  |  |
| 1.6 | 2005年11月 | 1.5 + Array extras + Array and String generics + E4X |  | 1.5 |  |  | 3.0, 3.1 |  |
| 1.7 | 2006年10月 | 1.6 + Pythonic generators + Iterators + let |  | 2.0 |  |  | 3.2, 4.0 | 1.0 |
| 1.8 | 2008年6月 | 1.7 + Generator expressions + Expression closures |  | 3.0 |  | 11.50 |  |  |
| 1.8.1 |  | 1.8 + Native JSON support + Minor Updates |  | 3.5 |  |  |  |  |
| 1.8.2 | 2009年6月22日 | 1.8.1 + Minor updates |  | 3.6 |  |  |  |  |
| 1.8.5 | 2010年7月27日 | 1.8.1 + ECMAScript 5 Compliance |  | 4 | 9 | 11.60 |  |  |



### 浏览器环境


    JavaScript 的宿主环境有多种，最常见的环境就是浏览器，另外还有服务器环境，也就是 Node 项目。


浏览器，主要提供的额外 API 可以分成三大类：


- 浏览器控制类：操作浏览器
- DOM 类：操作网页的各种元素
- Web 类：实现互联网的各种功能



宿主环境是服务器，则会提供各种操作系统的 API，比如文件操作 API、网络通信 API等等。
