
```
[官网]

	: http://www.ecma-international.org/

	: https://developer.mozilla.org/fr/docs/Web/JavaScript/Language_Resources

[文档]

	: http://es6.ruanyifeng.com/

[参考文档]
// https://www.runoob.com/w3cnote/es6-tutorial.html
// https://www.w3cschool.cn/ecmascript/8j1d1q68.html
# http://www.dba.cn/book/ecmascript/

// https://www.ibm.com/developerworks/cn/web/1305_chengfu_ecmascript5/
```

[ECMAScript  - 262 2018 规范.pdf]()

[ES6标准入门 第三版 阮一峰 201709.pdf]()

    ECMAScript 是一种由Ecma国际（前身为欧洲计算机制造商协会，European Computer Manufacturers Association）通过ECMA-262标准化的脚本程序设计语言。

    其往往被称为JavaScript或JScript，所以它可以理解为是JavaScript的一个标准,但实际上后两者是ECMA-262标准的实现和扩展。

    ECMAScript是由网景的布兰登·艾克 开发的一种脚本语言的标准化规范；最初命名为Mocha，后来改名为LiveScript，最后重命名为JavaScript。

### 历史版本

    1995年12月，升阳与网景联合发表了JavaScript。1996年11月，网景公司将JavaScript提交给欧洲计算机制造商协会进行标准化。ECMA-262的第一个版本于1997年6月被Ecma组织采纳。ECMA Script是ECMA-262标准化的脚本语言的名称。

    尽管JavaScript和JScript与ECMAScript兼容，但包含超出ECMA Script的功能。

    ECMAScript 是一种可以在宿主环境中执行计算并能操作可计算对象的基于对象的程序设计语言。ECMAScript最先被设计成一种Web脚本语言，用来支持Web页面的动态表现以及为基于Web的客户机—服务器架构提供服务器端的计算能力。但作为一种脚本语言， ECMAScript具备同其他脚本语言一样的性质，即“用来操纵、定制一个已存在系统所提供的功能，以及对其进行自动化”。

1998年6月，ECMAScript 2.0版发布。

1999年12月，ECMAScript 3.0版发布，成为JavaScript的通行标准，得到了广泛支持。

2007年10月，ECMAScript 4.0版草案发布，对3.0版做了大幅升级，预计次年8月发布正式版本。草案发布后，由于4.0版的目标过于激进，各方对于是否通过这个标准，发生了严重分歧。以Yahoo、Microsoft、Google为首的大公司，反对JavaScript的大幅升级，主张小幅改动；以JavaScript创造者Brendan Eich为首的Mozilla公司，则坚持当前的草案。

2008年7月，由于对于下一个版本应该包括哪些功能，各方分歧太大，争论过于激进，ECMA开会决定，中止ECMAScript 4.0的开发，将其中涉及现有功能改善的一小部分，发布为ECMAScript 3.1，而将其他激进的设想扩大范围，放入以后的版本，由于会议的气氛，该版本的项目代号起名为Harmony（和谐）。会后不久，ECMAScript 3.1就改名为ECMAScript 5。

2009年12月，ECMAScript 5.0版正式发布。Harmony项目则一分为二，一些较为可行的设想定名为JavaScript.next继续开发，后来演变成ECMAScript 6；一些不是很成熟的设想，则被视为JavaScript.next.next，在更远的将来再考虑推出。

2011年6月，ECMAscript 5.1版发布，并且成为ISO国际标准（ISO/IEC 16262:2011）。

2013年3月，ECMAScript 6草案冻结，不再添加新功能。新的功能设想将被放到ECMAScript 7。

2013年12月，ECMAScript 6草案发布。然后是12个月的讨论期，听取各方反馈。

2015年6月17日，ECMAScript 6 发布正式版本，即 _ECMAScript 2015_。

ECMA的第39号技术专家委员会（Technical Committee 39，简称TC39）负责制订ECMAScript标准，成员包括Microsoft、Mozilla、Google等大公司。TC39的总体考虑是，ES5与ES3基本保持兼容，较大的语法修正和新功能加入，将由JavaScript.next完成。

截止发布日期，JavaScript的官方名称是ECMAScript 2015，Ecma国际意在更频繁地发布包含小规模增量更新的新版本，下一版本将于2016年发布，命名为ECMAScript 2016。新版本将按照ECMAScript+年份的形式发布。

ES6是继ES5之后的一次主要改进，语言规范由ES5.1时代的245页扩充至600页。ES6增添了许多必要的特性，例如：模块和类，以及一些实用特性，例如Maps、Sets、Promises、生成器（Generators）等。尽管ES6做了大量的更新，但是它依旧完全向后兼容以前的版本，标准化委员会决定避免由不兼容版本语言导致的“web体验破碎”。结果是，所有老代码都可以正常运行，整个过渡也显得更为平滑，但随之而来的问题是，开发者们抱怨了多年的老问题依然存在。

截止发布日期，没有一款完全支持ES6的JavaScript代理（无论是浏览器环境还是服务器环境），所以热衷于使用语言最新特性的开发者需要将ES6代码转译为ES5代码。

等到主流浏览器完全实现ES6特性大概需要一年左右的时间，若想一睹各代理对于ES6特性的支持情况，我们推荐大家参考由 kangax 维护的 ECMAScript Compatibility Table 。

ECMAScript 2016的制定工作已经启动，许多 草案 已被提交到委员会，包括以下这些：异步方法、定型对象、并行JavaScript、类修饰符以及observables。虽然委员会正在积极评估这些特性，但我们无法预知它们的未来，其中一些会加入到下一版规范，另一些会加入未来的其它规范，剩下的将最终被遗弃。 TC39进程 解释了新特性从开始到最终被语言采用所经历的各种阶段。

### 思维导图

![](../../imgs/1572508174856-ed4332bf-5cc6-49da-8a6f-e9181e7faf2c.jpeg#align=left&display=inline&height=4344&originHeight=4344&originWidth=914&size=0&status=done&width=914)
