# ES6 语法基础 (ECMAScript 5.1 & ES6)

> ES6 语法学习, 及基本案例实现

## 运行

> - run
> node xx.js

## 案例

### 语法基础

#### 基本数据结构

> 共有六种数据结构 (number, string, boolean, undefined, null, object) , ES6 新增 Symbol
>
> 数值, 字符串, 布尔值
> null, undefined, 对象
> 函数
> 数组

> 字符串 (约定 JavaScript 语言的字符串只使用单引号)
> - length 属性返回字符串的长度
> - btoa()
> - atob()
> - encodeURIComponent()
> - decodeURIComponent()

> 对象 (object, 键值对的集合, 是一种无序的复合数据集合)
> - 对象的定义 (成员, 键名(属性, property), 键值) (对象的所有键名都是字符串(ES6 又引入了 Symbol 值也可以作为键名)) (属性的值为函数, 通常把这个属性称为“方法”, 它可以像函数那样调用)
> - 属性操作 (点运算符, 方括号运算符)
>
> - Object.keys() 方法, 查询对象属性
> - delete()      删除属性 (只能删除对象本身的属性, 无法删除继承的属性)
> - in 运算符      查询对象属性是否存在 (不能识别哪些属性是对象自身的，哪些属性是继承的)
> - hasOwnProperty() 判断对象属性是否为自身属性
> - for...in       对象属性遍历

> 函数
> - 函数定义
> - 函数调用 (圆括号运算符, return 返回函数结果, 没有返回 undefined)
> - 函数属性
>   - name 函数名
>   - length 返回函数预期传入的参数个数，即函数定义之中的参数个数
>   - toString 返回函数源码
>
> - 函数作用域
>   - 作用域(scope)指的是变量存在的范围, ES5只有两种作用域: 一种是全局作用域; 另一种是函数作用域，变量只在函数内部存在。ES6 又新增了块级作用域
>   - (函数执行时所在的作用域，是定义时的作用域，而不是调用时所在的作用域)
>   - 闭包 (closure) (在函数外部, 需要得到函数内部的值, 闭包就是将函数内部和函数外部连接起来的一座桥梁)
>
> - 函数参数
>   - 函数参数如果是原始类型的值 (数值、字符串、布尔值), 传递方式是传值传递, 复合类型的值是传址传递 (pass by reference)
>   - argumentsu 参数对象, 包含了函数运行时的所有参数

> 数组
> - 定义, 按次序排列的一组值。每个值的位置都有编号(从0开始), 整个数组用方括号表示。本质上，数组属于一种特殊的对象。
> - 数组属性
>   - length 属性, 返回数组的成员数量, 该属性是一个动态的值, 等于键名中的最大整数加上1, 表明数组是一种动态的数据结构，可以随时增减数组的成员
>   - 
> - in 运算符, 检查某个键名是否存在的运算符, 如果数组的某个位置是空位，in运算符返回false
> - for...in 遍历数组 (不仅会遍历数组所有的数字键, 还会遍历非数字键)
>
> - 空元素

#### 基本的语法构造 (操作符、控制结构、语句)
>
> 语句 (statement, 是为了完成某种任务而进行的操作)
> - 赋值语句
> - 表达式 (expression)
> - 控制语句
>
> 变量
> - 标识符 (identifier, 指的是用来识别各种值的合法名称, 包括变量名、函数名等)
> - 变量提升 (变量的声明语句，都会被提升到代码的头部，这就叫做变量提升(hoisting))
>
> 区块 (block, 使用大括号，将多个相关的语句组合在一起)
> - 作用域 (scope, 区块对于var命令不构成单独的作用域，与不使用区块的情况没有任何区别)
>
> 控制语句
> - 条件语句 (if, if-else, switch-case-default)
> - 跳转语句 (break, continue)
> - 三元运算符 ( ?: )
> - 循环语句 (while, fo-while, for)

### 标准库

#### 常用方法

> 类型判断运算符
> - typeof 运算符 (返回一个值的数据类型)
> - instanceof 运算符 (验证, 一个对象是否为指定的构造函数的实例)
> - Object.prototype.toString 方法、

> 全局函数 - 数值相关
> - parseInt   将字符串转为整数, 进制转换
> - parseFloat 将一个字符串转为浮点数
> - isNaN()    判断一个值是否为NaN (判断NaN更可靠的方法是, 利用NaN为唯一不等于自身的值的这个特点, 进行判断)
> - isFinite() 判断某个值是否为正常的数值

> 定时器 (timer)
>
> - setTimeout()     指定某个函数或某段代码，在多少毫秒之后执行
> - setInterval()    指定某个任务每隔一段时间就执行一次, 也就是无限次的定时执行。
> - clearTimeout()   取消定时器
> - clearInterval()  取消定时器
>
> - debounce 函数 (防抖动)

#### 对象 Object

> - Object
>   - 函数 Object(), 将传入数据转换成对象, 如果传入的是对象直接返回
>   - 构造函数, new Object(), 实例化一个对象, (简写: var obj = {};)

> - Object 静态方法
>
>  - Object.keys() 遍历对象的属性, 获取对象自身的(而不是继承的)所有属性名。(只返回可枚举的属性);
>  - Object.getOwnPropertyNames() 遍历对象的属性, 获取对象自身的(而不是继承的)所有属性名。(即返回可枚举也返回不可枚举属性);
>
>  - 对象属性模型的相关方法
>    - Object.getOwnPropertyDescriptor()  获取某个属性的描述对象
>    - Object.defineProperty()            通过描述对象, 定义某个属性
>    - Object.defineProperties()          通过描述对象, 定义多个属性
>  - 控制对象状态的相关方法
>    - Object.preventExtensions() 防止对象扩展
>    - Object.isExtensible()      判断对象是否可扩展
>    - Object.seal()              禁止对象配置
>    - Object.isSealed()          判断一个对象是否可配置
>    - Object.freeze()            冻结一个对象
>    - Object.isFrozen()          判断一个对象是否被冻结
>  - 原型链相关方法
>    - Object.create()            该方法可以指定原型对象和属性，返回一个新的对象
>    - Object.getPrototypeOf()    获取对象的Prototype对象

> - Object 实例方法 (定义在Object.prototype对象)
>
>  - Object.prototype.valueOf()         返回当前对象对应的值 (默认情况下返回对象本身, 用于自动类型转换时会默认调用这个方法)
>  - Object.prototype.toString()        返回当前对象对应的字符串形式 (默认情况下返回类型字符串, 当对象用于字符串加法时会自动调用toString方法)
>  - Object.prototype.toLocaleString()  返回当前对象对应的本地字符串形式
>  - Object.prototype.hasOwnProperty()  判断, 某个属性是当前对象自身的属性, 还是继承自原型对象的属性
>  - Object.prototype.isPrototypeOf()   判断, 当前对象是否为另一个对象的原型
>  - Object.prototype.propertyIsEnumerable() 判断某个属性是否可枚举, 判断某个属性是否可遍历, 只能判断对象自身属性

> - 属性描述对象 (ttributes object, JS 提供的一个内部数据结构, 用来描述对象的属性, 控制它的行为)
>
> - Object.getOwnPropertyDescriptor()  获取某个属性的描述对象 (只能用于对象自身的属性, 不能用于继承的属性)
> - Object.getOwnPropertyNames()       遍历对象的属性, 获取对象自身的(而不是继承的)所有属性名。(即返回可枚举也返回不可枚举属性);
> - Object.defineProperty()            通过描述对象, 定义某个属性 (通过属性描述对象, 定义或修改一个属性, 然后返回修改后的对象)
> - Object.defineProperties()          通过描述对象, 定义多个属性
> - Object.prototype.propertyIsEnumerable() 判断某个属性是否可枚举

> - 元属性
>
>  - value        该属性的属性值, 默认为undefined (一旦定义了取值函数get或存值函数set，就不能将writable属性设为true, 或者同时定义value属性, 否则会报错)
>  - writable     表示属性值(value)是否可改变(即是否可写), 默认为 true
>  - enumerable   表示该属性是否可遍历, 默认为true
>  - configurable 可配置性, 控制了属性描述对象的可写性。 默认为true
>  - get 存取器, 取值, 函数, 表示该属性的取值函数 (getter), 默认为 undefined
>  - set 存取器, 存值, 函数，表示该属性的存值函数 (setter), 默认为 undefined

> - 存取器
>

> - 控制对象状态
>   - Object.preventExtensions() 防止对象扩展 (使得一个对象无法再添加新的属性)
>   - Object.isExtensible()      判断对象是否可扩展
>   - Object.seal()              禁止对象配置 (使得一个对象既无法添加新属性, 也无法删除旧属性, 只是禁止新增或删除属性，并不影响修改某个属性的值)
>   - Object.isSealed()          判断一个对象是否可配置
>   - Object.freeze()            冻结一个对象 (使得一个对象无法添加新属性、无法删除旧属性、也无法改变属性的值，使得这个对象实际上变成了常量)
>   - Object.isFrozen()          判断一个对象是否被冻结

#### 数组 Array

> - 构造函数 (Array(), new Array(), [])

> - 静态方法
>   - Array.isArray() 判断是否为数组

> - 实例方法
>
>   - valueOf()  对该对象求值, 返回数组本身
>   - toString() 返回数组的字符串形式
>   - push()     在数组的末端添加一个或多个元素, 并返回添加新元素后的数组长度, 会改变原数组
>   - pop()      删除数组的最后一个元素, 并返回该元素, 会改变原数组
>   - shift()    用于删除数组的第一个元素，并返回该元素。注意，该方法会改变原数组。
>   - unshift()  在数组的第一个位置添加元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。
> // push 和 pop 结合使用, 就构成了 “后进先出” 的栈结构（stack）
> // push() 和 shift() 结合使用, 就构成了“先进先出” 的队列结构（queue）
>   - join()     以指定参数作为分隔符，将所有数组成员连接为一个字符串返回。如果不提供参数，默认用逗号分隔。数组成员是undefined或null或空位，会被转成空字符串
>   - concat()   用于多个数组的合并。它将新数组的成员，添加到原数组成员的后部，然后返回一个新数组，原数组不变。
>   - reverse()  用于颠倒排列数组元素，返回改变后的数组。注意，该方法将改变原数组。
>   - slice()    用于提取目标数组的一部分，返回一个新数组，原数组不变。
>   - splice()   用于删除原数组的一部分成员，并可以在删除的位置添加新的数组成员，返回值是被删除的元素。注意，该方法会改变原数组。
>   - sort()     对数组成员进行排序，默认是按照字典顺序排序。排序后，原数组将被改变。
>   - map()      将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回。
>   - forEach()  对数组的所有成员依次执行参数函数, 不返回值，只用来操作数据
>   - filter()   用于过滤数组成员，满足条件的成员组成一个新数组返回, 返回结果为true的成员组成一个新数组返回。该方法不会改变原数组。
>   - some(), every() 返回一个布尔值，表示判断数组成员是否符合某种条件。
>   - reduce()，reduceRight() 依次处理数组的每个成员，最终累计为一个值
>   - indexOf()      返回给定元素在数组中第一次出现的位置，如果没有出现则返回-1, 接受第二个参数，表示搜索的开始位置
>   - lastIndexOf()  返回给定元素在数组中最后一次出现的位置，如果没有出现则返回-1

#### 字符串 String

> - 构造函数 ( String(), new String(), '' )

> - 静态方法
>   - String.fromCharCode() 返回 Unicode 码点组成的字符串

> - 实例属性
>   - String.prototype.length 返回字符串的长度

> - 实例方法
>   - String.prototype.charAt()      返回指定位置的字符，参数是从0开始编号的位置, 这个方法完全可以用数组下标替代
>   - String.prototype.charCodeAt()  返回字符串指定位置的 Unicode 码点（十进制表示）
>   - String.prototype.concat()      用于连接两个字符串，返回一个新字符串，不改变原字符串
>   - String.prototype.slice()       用于从原字符串取出子字符串并返回，不改变原字符串
>   - String.prototype.substring()   用于从原字符串取出子字符串并返回，不改变原字符串
>   - String.prototype.substr()      用于从原字符串取出子字符串并返回，不改变原字符串
>   - String.prototype.indexOf()     用于确定一个字符串在另一个字符串中第一次出现的位置，返回结果是匹配开始的位置。如果返回-1，就表示不匹配。
>   - String.prototype.lastIndexOf() 用于确定一个字符串在另一个字符串中最后一次出现的位置，返回结果是匹配开始的位置。如果返回-1，就表示不匹配。
>   - String.prototype.trim()        用于去除字符串两端的空格，返回一个新字符串，不改变原字符串。
>   - String.prototype.toLowerCase() 用于将一个字符串全部转为小写
>   - String.prototype.toUpperCase() 用于将一个字符串全部转为大写
>   - String.prototype.match()       用于确定原字符串是否匹配某个子字符串，返回一个数组，成员为匹配的第一个字符串
>   - String.prototype.search()      用法基本等同于match，但是返回值为匹配的第一个位置
>   - String.prototype.replace()
>   - String.prototype.split()       按照给定规则分割字符串，返回一个由分割出来的子字符串组成的数组。
>   - String.prototype.localeCompare() 用于比较两个字符串


#### 数学 Math

> - 静态属性
>   - Math.E      常数e
>   - Math.LN2    2 的自然对数。
>   - Math.LN10   10 的自然对数。
>   - Math.LOG2E  以 2 为底的e的对数。
>   - Math.LOG10E 以 10 为底的e的对数。
>   - Math.PI     常数π
>   - Math.SQRT1_2  0.5 的平方根。
>   - Math.SQRT2    2 的平方根。

> - 静态方法
>   - Math.abs()     绝对值
>   - Math.max()     最大值
>   - Math.min()     最小值
>   - Math.floor()   向下取整
>   - Math.ceil()    向上取整
>   - Math.round()   四舍五入
>   - Math.pow()     幂运算
>   - Math.sqrt()    平方根
>   - Math.log()     自然对数
>   - Math.exp()     e的指数
>   - Math.random()  随机数, 返回0到1之间的一个伪随机数，可能等于0，但是一定小于1
>   - 三角函数方法
>     - Math.sin()   返回参数的正弦（参数为弧度值）
>     - Math.cos()   返回参数的余弦（参数为弧度值）
>     - Math.tan()   返回参数的正切（参数为弧度值）
>     - Math.asin()  返回参数的反正弦（返回值为弧度值）
>     - Math.acos()  返回参数的反余弦（返回值为弧度值）
>     - Math.atan()  返回参数的反正切（返回值为弧度值）


#### 时间 Date

> 普通函数 ( Date(), new Date())

> - 静态方法
>   - Date.now()    返回当前时间距离时间零点（1970年1月1日 00:00:00 UTC）的毫秒数
>   - Date.parse()  用来解析日期字符串，返回该时间距离时间零点（1970年1月1日 00:00:00）的毫秒数。
>   - Date.UTC()    接受年、月、日等变量作为参数，返回该时间距离时间零点（1970年1月1日 00:00:00 UTC）的毫秒数。

> - 实例方法
>   - Date.prototype.valueOf()
>   - to 类方法   从Date对象返回一个字符串，表示指定的时间。
>   - get 类方法  获取Date对象的日期和时间。
>   - set 类方法  设置Date对象的日期和时间

#### RegExp


#### JSON

> - 静态方法
>   - JSON.stringify()  用于将一个值转为 JSON 字符串
>   - JSON.parse        用于将 JSON 字符串转换成对应的值


### 面向对象

> - 类及对象

> - 对象体系 (对象体系，不是基于“类”的，而是基于构造函数 (constructor) 和原型链 (prototype))
>
>   - 构造函数 (constructor, 对象的模板, 专门用来生成实例对象的函数, 描述实例对象的基本结构) 
>     - new 命令 (执行构造函数, 返回一个实例对象) (构造函数, 有自己的特征, 内部使用 this 关键字, 且生成对象 必须使用 new 关键字)
>     - this (this就是函数运行时所在的对象(环境), JS支持运行环境动态切换, this 的指向是动态的, 没有办法事先确定到底指向哪个对象)

> - 绑定this
>   - Function.prototype.call()  指定函数内部this的指向（即函数执行时所在的作用域），然后在所指定的作用域中，调用该函数
>   - Function.prototype.apply() 改变this指向, 然后再调用该函数。区别是, 它接收一个数组作为函数执行时的参数。
>   - Function.prototype.bind()  用于将函数体内的this绑定到某个对象, 然后返回一个新函数

> - Object 对象的相关方法
>   - Object.getPrototypeOf() 返回参数对象的原型。这是获取原型对象的标准方法。
>   - Object.setPrototypeOf() 参数对象设置原型，返回该参数对象。
>   - Object.create() 该方法接受一个对象作为参数，然后以它为原型，返回一个实例对象。该实例完全继承原型对象的属性。
>   - Object.prototype.isPrototypeOf() 判断该对象是否为参数对象的原型
>   - Object.prototype.__proto__
>   - Object.getOwnPropertyNames()
>   - Object.prototype.hasOwnProperty()

### 异步操作

> - 事件机制 (Event Loop)
>   - 任务队列 (task queue)
>   - 同步任务 (synchronous) 和 异步任务 (asynchronous)

> - 回调函数 (是异步操作最基本的方法)
>  // 优点是简单、容易理解和实现
>  // 缺点是不利于代码的阅读和维护, 各个部分之间高度耦合, 使得程序结构混乱、流程难以追踪, 而且每个任务只能指定一个回调函数。

> - 事件监听 (事件驱动模式)
>  // 优点是比较容易理解, 可以绑定多个事件, 每个事件可以指定多个回调函数, 而且可以“去耦合”, 有利于实现模块化
>  // 缺点是整个程序都要变成事件驱动型, 运行流程会变得很不清晰。阅读代码的时候, 很难看出主流程。

> - 发布/订阅 (发布订阅模式 publish-subscribe pattern / 观察者模式 observer pattern)


### 异步操作的流程控制

> - Promise (JS 异步操作解决方案, 为异步操作提供统一接口, 使得异步操作具备同步操作的接口)

> - 实例方法
>   - Promise.prototype.then()


### 宿主环境 API

#### 浏览器环境

> 浏览器控制类: 操作浏览器
> DOM 类: 操作网页的各种元素
> Web 类: 实现互联网的各种功能


#### 服务端 Node环境

> 操作系统的 API, 比如文件操作 API、网络通信 API
