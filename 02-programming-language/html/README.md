# HTML

> 超文本标记语言 (HyperText Markup Language), 描述网页的一种语言。

> 定义了网页内容的含义和结构


## 资源

> [规范](https://html.spec.whatwg.org/multipage/)

> [Web 开发技术](https://developer.mozilla.org/zh-CN/docs)
>
>  - [](https://developer.mozilla.org/zh-CN/docs/Learn/Getting_started_with_the_web)
>
>  - [HTML（超文本标记语言）初学者教程](https://developer.mozilla.org/zh-CN/docs/Web/HTML)
>
>  - [Web 开发技术](https://developer.mozilla.org/zh-CN/docs)


> [](https://www.w3.org/TR/html51/)

> [](https://www.w3school.com.cn/html/index.asp)
>
> [](https://www.runoob.com/html/html-tutorial.html)
>
> [](https://www.jianshu.com/p/42285a60545e)

> 组件库
>
> - layui
> - element-ui


## 简介

HTML, HyperText Markup Language, 超文本标记语言, 描述网页的一种语言。是一种标识性的语言。它包括一系列标签，通过这些标签可以将网络上的文档格式统一，使分散的Internet资源连接为一个逻辑整体。是用来标记Web信息如何展示以及其他特性的一种语法规则，它最初于1989年由GERN的Tim Berners-Lee发明。

HTML基于更古老一些的语言SGML定义，并简化了其中的语言元素。这些元素用于告诉浏览器如何在用户的屏幕上展示数据。

自1990年以来，HTML就一直被用作WWW的信息表示语言，使用HTML语言描述的文件需要通过WWW浏览器显示出效果。HTML是一种建立网页文件的语言，通过标记式的指令(Tag)，将影像、声音、图片、文字动画、影视等内容显示出来。

超级文本标记语言，是标准通用标记语言下的一个应用，也是一种规范，一种标准，它通过标记符号来标记要显示的网页中的各个部分。


超文本是由HTML命令组成的描述性文本，HTML命令可以说明文字，图形、动画、声音、表格、链接等。是一种组织信息的方式，它通过超级链接方法将文本中的文字、图表与其他信息媒体相关联。

- 标签, HTML 标记标签通常被称为 HTML 标签 (HTML Tag);

- 元素, 通常和标签一样都是描述同样的意思, 但严格来说其包含, 开始标签和结束标签;

- 属性, 元素可以设置属性, 提供附加信息, 以键值对表示。

- 响应式 : RWD, Responsive Web Design, 响应式 Web 设计

能够以可变尺寸传递网页, 对于平板和移动设备是必需的, 简言之, 同一个web网页, 根据浏览设备的不同(设备显示长度宽度等), 自动调节页面显示效果和参数


### 历史版本

HTML 1.0：在1993年6月作为互联网工程工作小组(IETF)工作草案发布。

HTML 2.0：1995年1 1月作为RFC 1866发布，于2000年6月发布之后被宣布已经过时。

HTML 3.2：1997年1月14日，W3C推荐标准。

HTML 4.0：1997年12月18日，W3C推荐标准。

HTML 4.01（微小改进）：1999年12月24日，W3C推荐标准。

HTML 5：HTML5是公认的下一代Web语言，极大地提升了Web在富媒体、富内容和富应用等方面的能力，被喻为终将改变移动互联网的重要推手

在 W3C 推出 DOM 标准之前，市场上已经流行了不同版本的 DOM 规范，主要包括 IE 和 Netscape 两个浏览器厂商各自制订的私有规范，这些规范定义了一套文档结构操作的基本方法。

虽然这些规范存在差异，但是思路和用法基本相同，如文档结构对象、事件处理方式、脚本化样式等。习惯上，我们把这些规范称为 DOM 0 级，虽然这些规范没有同义并实现标准化，但是得到所有浏览器的支持并被广泛应用。

1998 年 W3C 对 DOM 进行标准化，并先后推出了 3 个不同的版本，每个版本都是在上一个版本的基础上进行完善和扩展。但是在某些情况下，不同版本之间可能会存在不兼容的规定。

#### DOM 1 级

  1998 年 10 月，W3C 推出 DOM 1.0 版本规范，作为推荐标准进行正式发布，主要包括两个子规范。

- DOM Core（核心部分）：把 XML 文档设计为树形节点结构，并为这种结构的运行机制制订了一套规范化标准，同时定义了创建、编辑、操纵这些文档结构的基本属性和方法。

- DOM HTML：针对 HTML 文档、标签集合，以及与个别 HTML 标签相关的元素定义了对象、属性和方法。

#### DOM 2 级

2000 年 11 月，W3C 正式发布了更新后的 DOM 核心部分，并在这次发布中添加了一些新规范，于是人们就把这次发布的 DOM 称为 2 级规范。

2003 年 1 月，W3C 又正式发布了对 DOM HTML 子规范的修订，添加了针对 HTML 4.01 和 XHTML 1.0 版本文档中很多对象、属性和方法。W3C 把新修订的 DOM 规范同义称为 DOM 2.0 推荐版本，该版本主要包括 6 个推荐子规范。

- DOM2 Core：继承于 DOM Core 子规范，规定了 DOM 文档结构模型，添加了更多的特性，如针对命名空间的方法等。
- DOM2 HTML：继承于 DOM HTML，规定了针对 HTML 的 DOM 文档结构模型，并添加了一些属性。
- DOM2 Events：规定了与鼠标相关的事件（包括目标、捕获冒泡和取消）的控制机制，但不包含与键盘相关事件的处理部分。
- DOM2 Style（或 DOM2 CSS）：提供了访问和操纵所有与 CSS 相关的样式及规则的能力。
- DOM2 Traversal 和 DOM2 Range：DOM2 Traversal 规范允许开发人员通过迭代方式访问 DOM，DOM2 Range 规范允许对指定范围的内容进行操作。
- DOM2 Views：提供了访问和更新文档表现（视图）的能力。

#### DOM 3 级

2004 年 4 月，W3C 发布了 DOM3 版本。DOM3 版本主要包括以下 3 个推荐子规范。

- DOM3 Core：继承于 DOM2 Core，并添加了更多的新方法和属性，同时修改了已有的一些方法。

- DOM3 Load and Save：提供将 XML 文档的内容加载到 DOM 文档中，以及将 DOM 文档序列化为 XML 文档的能力。

- DOM3 Validation：提供了确保动态生成的文档的有效性的能力，即如何符合文档类型声明。

### HTML5

```
[H5 包含了一列的标准，一共包含了十大类别]

离线 Offilne
存储 Storatge
连接 Connectivity
文件访问 File Access
语义 Semantics
音视频 Audio/Video
3D图形 3D/Graphics
展示 Presentation
性能 Performance
其他 NutsAndBolts
```


## 纲目

> 1. html
>
> 2. 标签 (tag), HTML 标记标签通常被称为 HTML 标签 (HTML Tag); 元素 (element), 通常和标签一样都是描述同样的意思, 但严格来说其包含, 开始标签和结束标签;
>
>   - 结构
>   - 文本
>   - 表格
>   - 列表
>   - 表单
>   - 块
>   - 多媒体
>   - 注释
>
> 3. 属性 (attribute), 元素可以设置属性, 提供附加信息, 以键值对表示; 样式 (style)
>



































- 块级元素 (block level element), 块级元素在浏览器显示时，通常会以新行来开始(结束)
- 内联元素 (inline element), 内联元素在显示时通常不会以新行开始

``` 重定向定义
<meta http-equiv="Refresh" content="5; url=http://www.baidu.com" />
```





	//: <s>	  不赞成使用。使用 <del> 代替
	//: <strike>	不赞成使用。使用 <del> 代替
	//: <u>	不赞成使用。使用样式（style）代替

//

	: <code>  定义计算机代码
	: <kbd>   定义键盘码
	: <samp>  定义计算机代码样本
	: <tt>    定义打字机代码
	: <var>	  定义变量
	: <pre>	  定义预格式文本

	//: <listing>	  不赞成使用。使用 <pre> 代替
	//: <plaintext>	不赞成使用。使用 <pre> 代替
	//：<xmp>	 不赞成使用。使用 <pre> 代替

// 引用、引用和术语

	: <abbr>    定义缩写
	: <acronym>	定义首字母缩写
	: <address>	定义地址
	: <bdo>     定义文字方向
	: <blockquote>  定义长的引用
	: <q>    定义短的引用语
	: <cite> 定义引用、引证
	: <dfn>  定义一个定义项目

[引用]

 : <q> 短引用, 定义短的引用

  : <blockquote> 长引用, 定义被引用的节

  : <abbr> 定义缩写或首字母缩略语
  
  : <dfn> 定义项目或缩写的定义
  
  : <cite> 定义著作的标题
  
  : <bdo> 定义双流向覆盖 (bi-directional override)

<abbr>    定义缩写或首字母缩略语
<address> 定义文档作者或拥有者的联系信息
<bdo>     定义文本方向
<blockquote>  定义从其他来源引用的节
<dfn>  定义项目或缩略词的定义
<q>    定义短的行内引用
<cite> 定义著作的标题

[计算机代码格式]

	: <kbd>  定义键盘输入
  
  : <samp>  定义计算机输出
  
  : <code>  定义编程代码, 元素不保留多余的空格和折行
  
  : <var>   定义数学变量

<code>	定义计算机代码文本
<kbd>	定义键盘文本
<samp>	定义计算机代码示例
<var>	定义变量
<pre>	定义预格式化文本

[字符实体]

	: 正确地显示预留字符, 需要使用字符实体 (character entities)
  # 不间断空格 &nbsp;	&#160;
	<	小于号	&lt;	&#60;
	>	大于号	&gt;	&#62;
	&	和号	&amp;	&#38;
	"	引号	&quot;	&#34;
	'	撇号 	&apos; (IE不支持)	&#39;
	￠	分（cent）	&cent;	&#162;
	£	镑（pound）	&pound;	&#163;
	¥	元（yen）	&yen;	&#165;
	€	欧元（euro）	&euro;	&#8364;
	§	小节	&sect;	&#167;
	©	版权（copyright）	&copy;	&#169;
	®	注册商标	&reg;	&#174;
	™	商标	&trade;	&#8482;
	×	乘号	&times;	&#215;
	÷	除号	&divide;	&#247;
  // https://www.w3school.com.cn/tags/html_ref_entities.html

```


```
[超链接]

	: <a>
  # 属性, name href target
  # name 锚定义(anchor) ,  id 属性可以替代name属性

[脚本]

	: <script>
  # type 属性指定脚本的 MIME 类型, text/javascript
  # src 属性指向外部文件
  
  : <noscript>
  # 提供无法使用脚本时的替代内容 (浏览器禁用脚本时, 浏览器不支持客户端脚本时)
  
// 文件路径, 描述了网站文件夹结构中某个文件的位置
// 绝对路径, 相对路径

[]

	: URL - Uniform Resource Locator 统一资源定位器
  # 规则
  # scheme://host.domain:port/path/filename
  // scheme - 定义因特网服务的类型。最常见的类型是 http
  // host - 定义域主机（http 的默认主机是 www）
  // domain - 定义因特网域名，比如 w3school.com.cn
  // :port - 定义主机上的端口号（http 的默认端口号是 80）
  // path - 定义服务器上的路径（如果省略，则文档必须位于网站的根目录中）。
  // filename - 定义文档/资源的名称

	: 浏览器颜色
  // https://www.w3school.com.cn/html/html_colors.asp
  // https://www.w3school.com.cn/html/html_colornames.asp

```

### H5

```
[H5]

  : 文档类型
  # <!DOCTYPE>
  # H5规范文档类型声明 : <!DOCTYPE html>

[H5 新元素]

  : 语义元素 - 清楚地定义其描述及意义 (非语义元素 - div, span 无法提供关于其内容的信息)

// 了定义页面不同部分的新语义元素
	// 

// 定义页面不同部分
<section>	定义文档中的节, 主题的内容组，通常具有标题 (网站首页划分为简介、内容、联系信息等节)

<article>  定义文章, 独立的自包含内容, 具有有其自身的意义, 并且可以独立于网站其他内容进行阅读
<header>   定义文档或节的页眉, 文档或节规定页眉, 用作介绍性内容的容器
<footer>   定义文档或节的页脚, 包含文档的作者、版权信息、使用条款链接、联系信息等等
<nav>	     定义导航链接集合, 定义大型的导航链接块。
<aside>    定义页面内容以外的内容, 如侧栏, 内容应该与周围内容相关
<figure>     定义自包含内容，比如图示、图表、照片、代码清单等, 图片和标题组合
<figcaption> 定义 <figure> 元素的标题
<details>  定义用户能够查看或隐藏的额外细节
<main>	  规定文档的主内容
<mark>	  定义重要的或强调的文本
<summary>	定义 <details> 元素的可见标题
<time>	  定义日期/时间

[自定义标签 - 及浏览器标签兼容]

// 所有浏览器, 不论新旧, 都会自动把未识别元素当做行内元素来处理
// 自定义添加新元素
// 通过浏览器 <trick> 向 HTML 添加任何新元素

<!DOCTYPE html>
<html>

<head>
  <title>Creating an HTML Element</title>
  <script>document.createElement("myHero")</script>
  <style>
  myHero {
    display: block;
    background-color: #ddd;
    padding: 50px;
    font-size: 30px;
  } 
  </style> 
</head>

<body>

<h1>My First Heading</h1>

<p>My first paragraph.</p>

<myHero>My First Hero</myHero>

</body>
</html>

// 注意：Internet Explorer 8 以及更早的版本，不允许对未知元素添加样式。
// IE9 的早期版本会读取它（并理解它)
// 引用 shiv 代码的链接必须位于 <head> 元素中，因为 Internet Explorer 需要在读取之前认识所有新元素
<!--[if lt IE 9]>
  <script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
<![endif]-->
// Shiv 解决方案
<!DOCTYPE html>
<html>

<head>
  <title>Styling HTML5</title>
  
  <!--[if lt IE 9]>
  <script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
  <![endif]-->
</head>

<body>

<h1>My First Article</h1>

<article>
London is the capital city of England. 
It is the most populous city in the United Kingdom, 
with a metropolitan area of over 13 million inhabitants.
</article>

</body>
</html>

```

### 废弃说明

```
[废弃]

	: body 属性 : bgcolor 背景颜色 background 背景图片 text 文本

	: <center> 居中 \ <font> <basefont> 字体 \ <s> <strike> 删除线
  : <u>     下划线
  : align   定义文本的对齐方式
  : bgcolor 背景色
  : color   文本颜色

<acronym> <applet> <basefont> <big> <center> <dir> <font> <frame> <frameset> <noframes>
<strike> <tt>

```



[表单]

  # <input> 输入框 [list 预定义选项列表 type (text 文本, radio 单选, submit 提交) name value]
  // type (text 文本, radio 单选, checkbox 复选框, submit 提交, password 密码, button 按钮)
  // color date datetime datetime-local email month number range search tel time url week
  # <fieldset> <legend>
  # <select> 下拉列表, <option> 定义待选择的选项 [selected 属性定义预定义选项]
  # <textarea> 文本域 [name rows cols]
  # <button> 按钮 [type onclick ]
  # <datalist> 为input规定预定义选项列表 <keygen> <output>

// 表单属性
accept-charset	规定在被提交表单中使用的字符集（默认：页面字符集）。
action	规定向何处提交表单的地址（URL）（提交页面）。, 浏览器会基于用户之前的输入值自动填写值
autocomplete	规定浏览器应该自动完成表单（默认：开启）。
enctype	规定被提交数据的编码（默认：url-encoded）。
method	规定在提交表单时所用的 HTTP 方法（默认：GET）。
name	规定识别表单的名称（对于 DOM 使用：document.forms.name）。
novalidate	规定浏览器不验证表单。
target	规定 action 属性中地址的目标（默认：_self）。

// input
value    规定输入字段的初始值
readonly 规定输入字段为只读, 无法修改
disabled 规定输入字段应该被禁用, 不可用和不可点击, 不会被提交
required 规定输入字段是必需的(必需填写)
size     规定输入字段的宽度, 以字符计
maxlength 规定输入字段允许的最大长度, 输入控件不会接受超过所允许数的字符
max	     规定输入字段的最大值 // 规定 <input> 元素的最小值和最大值
min	     规定输入字段的最小值
pattern 规定通过其检查输入值的正则表达式 (regexp)
step	  规定输入字段的合法数字间隔
form 规定 <input> 元素所属的一个或多个表单, 如需引用一个以上的表单，请使用空格分隔的表单 id 列表
formaction 规定当提交表单时处理该输入控件的文件的 URL, 覆盖 <form> 元素的 action 属性
formenctype 规定当把表单数据（form-data）提交至服务器时如何对其进行编码
formmethod 定义用以向 action URL 发送表单数据（form-data）的 HTTP 方法
formnovalidate 规定在提交表单时不对 <input> 元素进行验证
formtarget 规定的名称或关键词指示提交表单后在何处显示接收到的响应
height width 高度和宽度, 仅用于 <input type="image">
list 引用的 <datalist> 元素中包含了 <input> 元素的预定义选项
multiple 规定允许用户在 <input> 元素中输入一个以上的值
placeholder 规定用以描述输入字段预期值的提示
autocomplete 规定表单或输入字段是否应该自动完成
novalidate 规定在提交表单时不对表单数据进行验证
autofocus 规定当页面加载时 <input> 元素应该自动获得焦点

<datalist>	定义输入控件的预定义选项
<keygen>	定义键对生成器字段(用于表单)
<output>	定义计算结果
