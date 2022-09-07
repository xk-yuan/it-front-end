# 数据类型 & 原生对象 & 基本库

>

## 资源

## 简介

> 数值 number | 字符串 string | 布尔值 boolean | 对象 object | Symbol | 未定义或不存在 undefined  | 空值 null

- 数值 number & Number对象
- 字符串 string & String对象
- 对象 object & Object对象
- 数组 array & Array对象
- 函数 function

> 属性描述对象 Attributes Object

- JS 内部数据结构, 用来描述对象的属性，控制它的行为，比如该属性是否可写、可遍历等等。每个属性都有自己对应的属性描述对象，保存该属性的一些元信息

> 元属性 (可以看作是控制属性的属性)

- value    是该属性的属性值, 默认为undefined
- writable 是一个布尔值, 表示属性值(value) 是否可写, 默认为true
- enumerable   布尔值, 表示该属性是否可遍历, 默认为true
- configurable 布尔值, 表示可配置性，默认为 true。设为 false, 将阻止某些操作改写该属性, configurable 属性控制了属性描述对象的可写性；比如无法删除该属性, 也不得改变该属性的属性描述对象(value属性除外)
- get 函数, 表示该属性的取值函数 (getter), 默认为undefined
- set 函数< 表示该属性的存值函数 (setter), 默认为undefined

- Object.getOwnPropertyDescriptor() 获取属性描述对象, 只能用于对象自身的属性, 不能用于继承的属性
- Object.getOwnPropertyNames() 返回一个数组, 成员是参数对象自身的全部属性的属性名, 不管该属性是否可遍历
- Object.defineProperty() 通过属性描述对象, 定义或修改一个属性, 然后返回修改后的对象。object 属性所在的对象 , propertyName 属性名, attributesObject 属性描述对象
- Object.defineProperties() 一次性定义或修改多个属性。一旦定义了取值函数get(或存值函数set), 就不能将writable属性设为true, 或者同时定义value属性
- Object.prototype.propertyIsEnumerable() 布尔值, 用来判断某个属性是否可遍历

> 存取器, 属性定义了存取器，那么存取的时候，都将执行对应的函数

> 对象的拷贝 (Object.defineProperty + Object.getOwnPropertyDescriptor + hasOwnProperty())

> 控制对象状态, 冻结对象的读写状态，防止对象被改变

- Object.preventExtensions() 对象无法再添加新的属性
- Object.isExtensible() 检查一个对象是否使用了Object.preventExtensions方法
- Object.seal() 使得一个对象既无法添加新属性，也无法删除旧属性
  - 实质是把属性描述对象的configurable属性设为false, 因此属性描述对象不再能改变
  - 只是禁止新增或删除属性, 并不影响修改某个属性的值
- Object.isSealed() 用于检查一个对象是否使用了Object.seal方法
- Object.freeze() 使得一个对象无法添加新属性、无法删除旧属性、也无法改变属性的值
  - 使得这个对象实际上变成了常量
- Object.isFrozen() 用于检查一个对象是否使用了Object.freeze方法
  - !局限性, 上面三个方法问题在于, 可以通过改变原型对象, 来为对象增加属性
  - 如果属性值是对象< 上面这些方法只能冻结属性指向的对象, 而不能冻结对象本身的内容


### 数值 number & Number对象

> 数值 number

- JavaScript 内部, 所有数字都是以64位浮点数形式储存, 即使整数也是如此。
- NaN、Infinity
- Number.MAX_VALUE、Number.MIN_VALUE

- parseInt()、parseFloat()、isNaN()、isFinite()

> Number对象

```javascript

	# Number对象是数值对应的包装对象，可以作为构造函数使用，也可以作为工具函数使用
  
  # 属性
  Number.POSITIVE_INFINITY 正的无限, 指向Infinity
  Number.NEGATIVE_INFINITY 负的无限, 指向-Infinity
	Number.NaN 表示非数值, 指向NaN
	Number.MAX_VALUE 表示最大的正数, 相应的, 最小的负数为 -Number.MAX_VALUE
	Number.MIN_VALUE 表示最小的正数, 即最接近0的正数, 在64位浮点数体系中为5e-324, 相应的, 最接近0的负数为 -Number.MIN_VALUE
	Number.MAX_SAFE_INTEGER 表示能够精确表示的最大整数, 即9007199254740991
	Number.MIN_SAFE_INTEGER 表示能够精确表示的最小整数, 即-9007199254740991

	# 实例方法
		Number.prototype.toString() 将一个数值转为字符串形式
		Number.prototype.toFixed()  先将一个数转为指定位数的小数, 然后返回这个小数对应的字符串
		Number.prototype.toExponential() 将一个数转为科学计数法形式
    Number.prototype.toPrecision() 将一个数转为指定位数的有效数字

  # 自定义方法
  // 数值的自定义方法，只能定义在它的原型对象Number.prototype上面，数值本身是无法自定义属性的

```

### [字符串 string & String对象]
```javascript
[字符串 string]

	# 字符串就是零个或多个排在一起的字符，放在单引号或双引号之中
  # 字符串默认只能写在一行内, 分成多行将会报错。
  # 字符串可以被视为字符数组, 因此可以使用数组的方括号运算符, 返回某个位置的字符(从0开始, 不能修改)
  // 方括号中的数字超过字符串的长度，或者方括号中根本不是数字，则返回 undefined
  
  # length 属性, 

  # \ 转义符
  // - \0 null  (\u0000)  | \b 后退键 (\u0008) | \f  换页符 (\u000C)
  // - \n 换行符 (\u000A) | \r 回车键（\u000D） | \t 制表符 (\u0009)
  // - \v 垂直制表符 (\u000B)  | \' 单引号 (\u0027) | \" 双引号 (\u0022)
  // - \\ 反斜杠     (\u005C)
  # \HHH | \xHH | \uXXXX - 字符表示(Unicode 码点)
  
  # Base64 转码 - 
  // btoa() 任意值转为 Base64 编码 、atob()：Base64 编码转为原来的值)
  // btoa(encodeURIComponent(str)) 、decodeURIComponent(atob(str)) # 非ASCII码, 需要转码

[String对象]

	# 原生提供的三个包装对象之一，用来生成字符串对象
  
  # String() , 工具方法使用, 将任意类型的值转为字符串 , 构造函数

	# 静态方法
		String.fromCharCode() 参数是一个或多个Unicode 码点数值, 返回值是这些码点组成的字符串

	# 实例属性
		String.prototype.length 字符串实例的length属性返回字符串的长度

	# 实例方法
		String.prototype.charAt() 返回指定位置的字符 (0开始编号) (可以使用数组下标替代)
		// 参数为负数, 或大于等于字符串的长度, charAt返回空字符串
		String.prototype.charCodeAt() 返回字符串指定位置的Unicode码点(十进制)，相当于String.fromCharCode()的逆操作
    // 参数为负数, 或大于等于字符串的长度, charCodeAt返回NaN
    String.prototype.concat() 连接两个字符串, 返回一个新字符串, 不改变原字符串
    String.prototype.slice()  从原字符串取出子字符串并返回, 不改变原字符串
    String.prototype.substring() 从原字符串取出子字符串并返回, 不改变原字符串
    String.prototype.substr() 从原字符串取出子字符串并返回, 不改变原字符串
    String.prototype.indexOf()
		// 确定一个字符串在另一个字符串中第一次出现的位置, 返回结果是匹配开始的位置, -1 表示不匹配
		String.prototype.lastIndexOf()
		// 确定一个字符串在另一个字符串中第一次出现的位置(从尾部开始匹配), 返回结果是匹配开始的位置, -1 表示不匹配
    String.prototype.trim() 去除字符串两端的空白符, 返回一个新字符串, 不改变原字符串
    String.prototype.toLowerCase() 将一个字符串全部转为小写, 返回一个新字符串，不改变原字符串
		String.prototype.toUpperCase() 将一个字符串全部转为大写, 返回一个新字符串，不改变原字符串
    String.prototype.match() 确定原字符串是否匹配某个子字符串, 返回一个数组, 成员为匹配的第一个字符串
		// 。如果没有找到匹配，则返回null
    String.prototype.search() 返回值为匹配的第一个位置。如果没有找到匹配，则返回-1
		String.prototype.replace() 替换匹配的子字符串, 一般情况下只替换第一个匹配
    String.prototype.split() 按照给定规则分割字符串, 返回一个由分割出来的子字符串组成的数组
    String.prototype.localeCompare() 比较两个字符串, 它返回一个整数 (考虑自然语言, 指定语言)
		// 如果小于0, 表示第一个字符串小于第二个字符串
		// 等于0, 表示两者相等
		// 大于0, 表示第一个字符串大于第二个字符串

```

### [对象 object & Object对象]

```javascript
[对象 object]

	# 对象就是一组“键值对”（key-value）的集合, 是一种无序的复合数据集合
  # define : var obj = {key:value, key:value}

  # 引用, 引用只局限于对象, 如果两个变量指向同一个原始类型的值。那么, 变量这时都是值的拷贝。

  # 键名, 对象的所有键名都是字符串(ES6又引入了 Symbol 值也可以作为键名), 非必须添加引号
  // 键名是数值, 会被自动转为字符串
  
  # 属性, 对象的每一个键名又称为“属性” (property), 它的“键值”可以是任何数据类型
  // 对象的属性之间用逗号分隔, 最后一个属性后面可以加逗号(trailing comma), 也可以不加
  // 属性可以动态创建, 不必在对象声明时就指定
  // V8 引擎规定, 如果行首是大括号, 一律解释为对象 | ({key:value, key:value})
  // 一个属性的值为函数, 通常把这个属性称为“方法”, 它可以像函数那样调用
  // 属性的值还是一个对象, 就形成了链式引用
  # 属性 - 读取
  // 点运算符 : obj.key
  // 方括号运算符 :  obj[key]
  // 方括号运算符使用时, 键名必须放在引号里面, 否则会被当作变量处理
  // 方括号运算符内部还可以使用表达式
  // 数值键名, 不能使用点运算符(因为会被当成小数点), 只能使用方括号运算符
  # 属性 - 赋值
  // 点运算符 : obj.key = value
  // 方括号运算符 :  obj[key] = value
  
  # Object.keys(obj) 获取对象所有属性名称
  # delete obj.key | delete(obj.key)  删除对象属性
  // 只能删除对象本身的属性, 无法删除继承的属性
  
  # in 运算符, 检查对象是否包含某个属性（注意，检查的是键名，不是键值
  // 不能识别哪些属性是对象自身的, 哪些属性是继承的
  # for-in 循环, 遍历一个对象的全部属性
  // 遍历的是对象所有可遍历(enumerable)的属性, 会跳过不可遍历的属性
  // 不仅遍历对象自身的属性，还遍历继承的属性

[Object对象]

	# 原生提供Object对象, JS中所有其他对象都继承自Object对象, 即都是Object的实例

  # Object对象的原生方法分成两类: Object本身的方法与Object的实例方法
  // 本身的方法, 就是直接定义在Object对象的方法
  // 实例方法就是定义在Object原型对象Object.prototype上的方法, 它可以被Object实例直接使用

	-> Object() 函数, 将任意值转为对象
	// 参数为空（或者为undefined和null），Object()返回一个空对象, 保证某个值一定是对象
	-> Object() 构造函数, 生成新对象 (new) (var obj = new Object() 等同于 var obj = {})

	# instanceof 运算符, 验证一个对象是否为指定的构造函数的实例
  
  # 静态方法(本身方法)
  	Object.keys() 获取对象自身且可枚举, 非继承的属性名 (遍历对象的属性)
  	Object.getOwnPropertyNames 获取对象自身所有, 非继承的属性名 (遍历对象的属性)
  // - 对象属性模型的相关方法
		Object.getOwnPropertyDescriptor() 获取某个属性的描述对象
		Object.defineProperty() 通过描述对象，定义某个属性。
		Object.defineProperties() 通过描述对象，定义多个属性。
  // - 控制对象状态的方法
		Object.preventExtensions()：防止对象扩展。
		Object.isExtensible()：判断对象是否可扩展。
		Object.seal()：禁止对象配置。
		Object.isSealed()：判断一个对象是否可配置。
		Object.freeze()：冻结一个对象。
		Object.isFrozen()：判断一个对象是否被冻结。
  // - 原型链相关方法
    Object.create()：该方法可以指定原型对象和属性，返回一个新的对象。
		Object.getPrototypeOf()：获取对象的Prototype对象。

	# 实例方法
  	Object.prototype.valueOf()
		// 返回当前对象对应的值 (默认情况下返回对象本身, 自动类型转换时会默认调用这个方法)
		Object.prototype.toString()
		// 返回当前对象对应的字符串形式 (默认情况下返回类型字符串)
    // 自动类型转换时, 可以得到想要的字符串形式(数组、字符串、函数、Date对象等都自定义了该方法))
    Object.prototype.toLocaleString()
		// 返回当前对象对应的本地字符串形式
    // 主要作用是, 让各种不同的对象实现自己版本的toLocaleString, 用来返回针对某些地域的特定的值
		// Array.prototype.toLocaleString()
    // Number.prototype.toLocaleString()
    // Date.prototype.toLocaleString()
    Object.prototype.hasOwnProperty()
		// 判断某个属性是否为当前对象自身的属性, 还是继承自原型对象的属性。
		Object.prototype.isPrototypeOf() 判断当前对象是否为另一个对象的原型
		Object.prototype.propertyIsEnumerable() 判断某个属性是否可枚举

[Object.prototype.toString({})]

	: 判断数据类型 ([object Object] , 第二个表示, 该值的构造函数)

	# 数值：返回[object Number]
	# 字符串：返回[object String]
	# 布尔值：返回[object Boolean]
	# undefined：返回[object Undefined]
	# null：返回[object Null]
	# 数组：返回[object Array]
	# arguments 对象：返回[object Arguments]
	# 函数：返回[object Function]
	# Error 对象：返回[object Error]
	# Date 对象：返回[object Date]
	# RegExp 对象：返回[object RegExp]
	# 其他对象：返回[object Object]

```

### [数组 array & Array对象]

```javascript
[数组 array]

	# 数组, 是按次序排列的一组值。每个值的位置都有编号(从0开始), 整个数组用方括号表示。
  // 数组的元素还是数组，就形成了多维数组
  # define : ['a', 'b', 'c'] , [[1, 2], [3, 4]]

  # 本质上，数组属于一种特殊的对象。typeof运算符会返回数组的类型是object。
  // 特殊性体现在, 它的键名是按次序排列的一组整数 (0, 1, 2 ...)
  // Object.keys(arr) - ["0", "1", "2"]

  # length 属性
  // 该属性是一个动态的值，等于键名中的最大整数加上 1
  // length属性是可写的。设置小于当前成员个数的值，=, 该数组的成员会自动减少到length设置的值。

[Array对象]

	# 原生对象，同时也是一个构造函数，可以用它生成新的数组
  
  # Array构造函数有一个很大的缺陷, 就是不同的参数, 会导致它的行为不一致

  # 静态方法
  	Array.isArray() 返回一个布尔值，表示参数是否为数组。它可以弥补typeof运算符的不足。

  # 实例方法
  	valueOf()  对该对象求值, 数组的valueOf方法返回数组本身
		toString() 数组的toString方法返回数组的字符串形式
    push() 数组的末端添加一个或多个元素, 并返回添加新元素后的数组长度, 方法会改变原数组
		pop()  删除数组的最后一个元素, 并返回该元素, 该方法会改变原数组
		// 对空数组使用pop方法, 不会报错, 而是返回undefined
		// push + pop 后进先出, 栈结构(stack)
		shift()    删除数组的第一个元素，并返回该元素。该方法会改变原数组
    // push + shift 先进先出, 队列结构(queue)
		unshift()  
		// 数组的第一个位置添加元素, 并返回添加新元素后的数组长度。该方法会改变原数组。
		join() 指定参数作为分隔符, 将所有数组成员连接为一个字符串返回 (默认使用逗号)
		// undefined或null或空位, 会被转成空字符串
		concat() 多数组合并, 新数组的成员, 添加到原数组成员的后部, 然后返回一个新数组, 原数组不变。
		// 除了数组作为参数，concat也接受其他类型的值作为参数，添加到目标数组尾部
		// 数组成员包括对象，concat方法返回当前数组的一个浅拷贝
		reverse() 颠倒排列数组元素，返回改变后的数组。注意，该方法将改变原数组。
    slice() 提取目标数组的一部分，返回一个新数组，原数组不变
    splice() 删除原数组的一部分成员，并可以在删除的位置添加新的数组成员，返回值是被删除的元素。注意，该方法会改变原数组。
    sort()  数组成员进行排序，默认是按照字典顺序排序。排序后，原数组将被改变。
    map()  将数组的所有成员依次传入参数函数, 然后把每一次的执行结果组成一个新数组返回
		// 数组有空位，map方法的回调函数在这个位置不会执行，会跳过数组的空位
		forEach() 对数组的所有成员依次执行参数函数。但是，forEach方法不返回值，只用来操作数据。
    // 跳过数组的空位
    filter() 过滤数组成员，满足条件的成员组成一个新数组返回
    some()，every() 类似“断言”（assert），返回一个布尔值，表示判断数组成员是否符合某种条件
    // some方法是只要一个成员的返回值是true，则整个some方法的返回值就是true，否则返回false。
    // every方法是所有成员的返回值都是true，整个every方法才返回true，否则返回false。
    // 对于空数组，some方法返回false，every方法返回true，回调函数都不会执行
    reduce()，reduceRight() 依次处理数组的每个成员，最终累计为一个值
    // reduce是从左到右处理（从第一个成员到最后一个成员），reduceRight则是从右到左（从最后一个成员到第一个成员）
    indexOf() 返回给定元素在数组中第一次出现的位置，如果没有出现则返回-1
		lastIndexOf() 返回给定元素在数组中最后一次出现的位置，如果没有出现则返回-1

```

### [函数 function]

```javascript
[函数 function]

	# 函数是一段可以反复调用的代码块。函数还能接受输入的参数，不同的参数会返回不同的值。
  // JavaScript 语言将函数看作一种值, 与其它值地位相同, 凡是可以使用值的地方, 就能使用函数。

  # define
  // - function name() {} // Function Declaration
  // - var name = function() {} // Function Expression
  // - var name = new Function( 'x', 'y', 'return x + y' );
  // 如果同一个函数被多次声明，后面的声明就会覆盖前面的声明
  // ES5 的规范, 不得在非函数的代码块中声明函数, 但可以使用函数表达式进行赋值

  # 函数调用, 圆括号运算符
  // 函数可以调用自身, 这就是递归(recursion)。
  
  # 函数名的提升
  // JS 引擎将函数名视同变量名, 采用function命令声明函数时, 整个函数会像变量声明一样, 被提升到代码头部。
  
  # name 属性、length 属性
  
  # toString() 方法
  
  # 函数作用域
  // 作用域(scope)指的是变量存在的范围, 
  // ES5只有两种作用域: 全局作用域, 变量在整个程序中一直存在; 函数作用域, 变量只在函数内部存在。
  // ES6 又新增了块级作用域
  // 函数外部声明的变量就是全局变量 (global variable), 它可以在函数内部读取
  // 函数内部定义的变量, 外部无法读取, 称为 “局部变量” (local variable)
  // 函数作用域内部也会产生“变量提升”现象。var命令声明的变量, 变量声明都会被提升到函数体的头部
  
  # 函数本身的作用域
  // 函数本身也是一个值, 也有自己的作用域。它的作用域与变量一样, 就是其声明时所在的作用域, 与其运行时所在的作用域无关。
	// 函数执行时所在的作用域, 是定义时的作用域, 而不是调用时所在的作用域。
	// 函数体内部声明的函数, 作用域绑定函数体内部 (这种机制，构成了“闭包”现象)

	# 参数
  // 函数参数不是必需的, Javascript 允许省略参数, 省略的参数的值就变为undefined
  // 传递方式 - 原始类型的值, 传递方式是传值传递 (passes by value)
  // - 复合类型的值, 传递方式是传址传递 (pass by reference)
  
  # arguments 对象, 包含了函数运行时的所有参数
  
  # 闭包 closure
  // 函数内部可以直接读取全局变量, 函数外部无法读取函数内部声明的变量
  // 定义在一个函数内部的函数 (函数的内部, 再定义一个函数)
  // (函数执行时所在的作用域, 是定义时的作用域, 而不是调用时所在的作用域)
  // (函数体内部声明的函数, 作用域绑定函数体内部)
  // (链式作用域 chain scope)
  // 闭包的最大用处有两个, 一个是可以读取函数内部的变量, 另一个就是让这些变量始终保持在内存中
	// 闭包的另一个用处，是封装对象的私有属性和私有方法

  # 立即调用的函数表达式 (IIFE)
  // - (function(){ /* code */ }());
  // - (function(){ /* code */ })();
  
```

### [Symbol]

```javascript
[]

	# ES6 引入了一种新的原始数据类型 Symbol, 表示独一无二的值
  // ES5 的对象属性名都是字符串, 这容易造成属性名的冲突
  
  # 方法
  Symbol.prototype.description 创建 Symbol 的时候，可以添加一个描述 (ES2019)
	Symbol.for()
  // 接受一个字符串作为参数，然后搜索有没有以该参数作为名称的 Symbol 值。
	// 如果有, 就返回, 否则新建一个以该字符串为名称的 Symbol 值，并将其注册到全局。
	Symbol.keyFor()
  // 返回一个已登记的 Symbol 类型值的key

	# 作为属性名
  // Symbol 值作为对象属性名时, 不能用点运算符
  // 对象的内部, 使用 Symbol 值定义属性时，Symbol 值必须放在方括号之中
  // Symbol 值作为属性名时，该属性还是公开属性，不是私有属性
  // 不可变遍历
  
  # 模块的 Singleton 模式
  // Singleton 模式指的是调用一个类，任何时候返回的都是同一个实例
  
  # 内置的 Symbol 值
  // - Symbol.hasInstance
  // - Symbol.isConcatSpreadable
  // - Symbol.species
  // - Symbol.match
  // - Symbol.replace
  // - Symbol.search
  // - Symbol.split
  // - Symbol.iterator
  // - Symbol.toPrimitive
  // - Symbol.toStringTag
  // - Symbol.unscopables
```

### 包装对象

```javascript
[]

	# 对象是JS语言最主要的数据类型
  # 三种原始类型的值(数值、字符串、布尔值), 在一定条件下, 会自动转为对象(原始类型的包装对象)

	# 实例方法
  valueOf() 返回包装对象实例对应的原始类型的值
  toString() 返回对应的字符串形式
  
  # 原始类型与实例对象的自动转换
  // 原始类型的值，可以自动当作包装对象调用，即调用各种包装对象的属性和方法
  // 自动转换生成的包装对象是只读的，无法修改, 调用结束后，包装对象实例会自动销毁

```

### Math & Date & RegExp & JSON & console

```javascript
[Math]

	# JS 原生对象, 提供各种数学功能
  // 该对象不是构造函数, 不能生成实例, 所有的属性和方法都必须在Math对象上调用
  // (如何定义构造函数和非构造函数)
  
  # 静态属性
  Math.E：常数e
	Math.LN2    2 的自然对数
	Math.LN10   10 的自然对数
	Math.LOG2E  以2为底的e的对数
	Math.LOG10E 以10为底的e的对数
	Math.PI   常数Pi
	Math.SQRT1_2  0.5 的平方根
	Math.SQRT2    2 的平方根

	# 静态方法
  Math.abs()    绝对值
  Math.ceil()   向上取整
  Math.floor()  向下取整
  Math.max() 最大值
  Math.min() 最小值
  Math.pow()  指数运算
  Math.sqrt() 平方根
  Math.log()  自然对数
  Math.exp()  e的指数
  Math.round()  四舍五入
  Math.random() 随机数

	# 三角函数方法
  Math.sin()  返回参数的正弦（参数为弧度值）
  Math.cos()  返回参数的余弦（参数为弧度值）
  Math.tan()  返回参数的正切（参数为弧度值）
  Math.asin()  返回参数的反正弦（返回值为弧度值）
  Math.acos()  返回参数的反余弦（返回值为弧度值）
  Math.atan()  返回参数的反正切（返回值为弧度值）

[Date]

	# JS 原生的时间库
  // 它以1970年1月1日00:00:00作为时间的零点, 可以表示的时间范围是前后各1亿天(单位为毫秒)

  # Date() 普通函数, 返回一个代表当前时间的字符串
  // "Tue Dec 01 2015 09:34:43 GMT+0800 (CST)"
  # Date() 构造函数 , 返回一个Date对象的实例
  // Date实例求值的时候, 默认调用的是toString()方法
  // 类型自动转换时, 转为数值, 为对应的毫秒数; 转为字符串, 则等于对应的日期字符串
  
  # 静态方法
  Date.now() 返回当前时间距离时间零点（1970年1月1日 00:00:00 UTC）的毫秒数，相当于 Unix 时间戳乘以1000
  Date.parse() 解析日期字符串，返回该时间距离时间零点（1970年1月1日 00:00:00）的毫秒数。
  Date.UTC() 接受年、月、日等变量作为参数，返回该时间距离时间零点（1970年1月1日 00:00:00 UTC）的毫秒数。
  
  # 实例方法
  Date.prototype.valueOf() 返回毫秒数, 等同于getTime方法
  to类   从Date对象返回一个字符串，表示指定的时间
  Date.prototype.toString() 返回一个完整的日期字符串
  Date.prototype.toUTCString() 返回对应的 UTC 时间，也就是比北京时间晚8个小时
  Date.prototype.toISOString() 返回对应时间的 ISO8601 写法
  Date.prototype.toJSON() 返回一个符合 JSON 格式的 ISO 日期字符串
  Date.prototype.toDateString() 返回日期字符串（不含小时、分和秒）
  Date.prototype.toTimeString() 返回时间字符串（不含年月日
  Date.prototype.toLocaleDateString() 返回一个字符串，代表日期的当地写法（不含小时、分和秒）
  Date.prototype.toLocaleTimeString() 返回一个字符串，代表时间的当地写法（不含年月日）
	get类  获取Date对象的日期和时间
  Date.prototype.getTime()  返回实例距离1970年1月1日00:00:00的毫秒数，等同于valueOf方法
  Date.prototype.getDate()  返回实例对象对应每个月的几号（从1开始）
  Date.prototype.getDay()   返回星期几，星期日为0，星期一为1，以此类推
  Date.prototype.getYear()  返回距离1900的年数
  Date.prototype.getFullYear()  返回四位的年份
  Date.prototype.getMonth()  返回月份（0表示1月，11表示12月）
  Date.prototype.getHours()  返回小时（0-23）
  Date.prototype.getMilliseconds()  返回毫秒（0-999）
  Date.prototype.getMinutes()  返回分钟（0-59）
  Date.prototype.getSeconds()  返回秒（0-59）
  Date.prototype.getTimezoneOffset()  返回当前时间与 UTC 的时区差异，以分钟表示，返回结果考虑到了夏令时因素。
	set类  设置Date对象的日期和时间
  Date.prototype.setDate(date)：设置实例对象对应的每个月的几号（1-31），返回改变后毫秒时间戳。
  Date.prototype.setYear(year): 设置距离1900年的年数。
  Date.prototype.setFullYear(year [, month, date])：设置四位年份。
  Date.prototype.setHours(hour [, min, sec, ms])：设置小时（0-23）。
  Date.prototype.setMilliseconds()：设置毫秒（0-999）。
  Date.prototype.setMinutes(min [, sec, ms])：设置分钟（0-59）。
  Date.prototype.setMonth(month [, date])：设置月份（0-11）。
  Date.prototype.setSeconds(sec [, ms])：设置秒（0-59）。
  Date.prototype.setTime(milliseconds)：设置毫秒时间戳。

[RegExp (正则表达式 Regular Expression)]

	# 实例属性
  RegExp.prototype.ignoreCase  返回一个布尔值, 表示是否设置了i修饰符。
  RegExp.prototype.global      返回一个布尔值, 表示是否设置了g修饰符。
  RegExp.prototype.multiline   返回一个布尔值, 表示是否设置了m修饰符
	//
  RegExp.prototype.lastIndex   返回一个数值, 表示下一次开始搜索的位置 (可读写)
  RegExp.prototype.source      返回正则表达式的字符串形式(不包括反斜杠, 只读)

	# 实例方法
	RegExp.prototype.test()  返回一个布尔值, 表示当前模式是否能匹配参数字符串
	RegExp.prototype.exec()  返回匹配结果, 返回一个数组, 成员是匹配成功的子字符串, 否则返回null

[JSON]

	# JS 原生对象, 用来处理 JSON 格式数据
  
  # 静态方法
  JSON.stringify() 用于将一个值转为 JSON 字符串
  // 忽略对象的不可遍历属性
  // 参数对象有自定义的toJSON方法, 那么JSON.stringify会使用这个方法的返回值作为参数
	JSON.parse() 将 JSON 字符串转换成对应的值

[console]

	# JS 原生对象, 它有点像 Unix 系统的标准输出stdout和标准错误stderr，可以输出各种信息到控制台
  // 调试程序, 显示网页代码运行时的错误信息
  // 提供了一个命令行接口, 用来与网页代码互动
  
  # 浏览器实现 (console对象的浏览器实现, 包含在浏览器自带的开发工具之中)
  
  # 静态方法
	console.log()   控制台输出信息
  // %s 字符串 、%d 整数 、%i 整数 、%f 浮点数、%o 对象的链接、%c CSS 格式字符串
	console.info() console.debug() console.warn() console.error()
	console.table()
	console.count()
	console.dir()
	console.dirxml()
	console.assert()
	console.time() console.timeEnd()
	console.group() console.groupEnd() console.groupCollapsed()
	console.trace() console.clear()

	# 命令行 API
  $_ 属性返回上一个表达式的值
  $0 - $4 , 控制台保存了最近5个在 Elements 面板选中的 DOM 元素
  $(selector)  返回第一个匹配的元素
  $$(selector) 返回选中的 DOM 对象
  $x(path) 方法返回一个数组，包含匹配特定 XPath 表达式的所有 DOM 元素
  inspect(object) 方法打开相关面板，并选中相应的元素，显示它的细节
  getEventListeners(object) 返回一个对象，该对象的成员为object登记了回调函数的各种事件
  keys(object)方法返回一个数组，包含object的所有键名
  values(object)方法返回一个数组，包含object的所有键值
  monitorEvents(object[, events]) 方法监听特定对象上发生的特定事件
  unmonitorEvents(object[, events]) 停止监听
  clear()：清除控制台的历史。
	copy(object)：复制特定 DOM 元素到剪贴板。
	dir(object)：显示特定对象的所有属性，是console.dir方法的别名。
	dirxml(object)：显示特定对象的 XML 形式，是console.dirxml方法的别名
	debugger 语句, 设置断点
```

### Set & Map (集合-数据结构)

```javascript
[Set]

	# ES6 提供了新的数据结构 Set, 类似于数组，但是成员的值都是唯一的, 没有重复值
  // 构造函数
  
  # 实例的属性
  Set.prototype.constructor  构造函数，默认就是Set函数
  Set.prototype.size         返回Set实例的成员总数
  
  # 实例方法
  // - 操作方法 (操作数据)
  Set.prototype.add(value)    添加某个值，返回 Set 结构本身
  Set.prototype.delete(value) 删除某个值，返回一个布尔值
  Set.prototype.has(value)    表示该值是否为Set的成员
  Set.prototype.clear()       清除所有成员
  // - 遍历方法
  // Set的遍历顺序就是插入顺序
  Set.prototype.keys()    返回键名的遍历器
	Set.prototype.values()  返回键值的遍历器
	Set.prototype.entries() 返回键值对的遍历器
	Set.prototype.forEach() 使用回调函数遍历每个成员
  // 扩展运算符（...）内部使用for...of循环，所以也可以用于 Set 结构
  // let arr = [...set];
  // 使用 Set 可以很容易地实现并集(Union)、交集(Intersect)和差集(Difference)

[WeakSet]

	# WeakSet 结构与 Set 类似，也是不重复的值的集合
  // WeakSet 的成员只能是对象，而不能是其他类型的值
  // WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用
  
  # 构造函数
  
  #
  WeakSet.prototype.add(value)     向 WeakSet 实例添加一个新成员。
	WeakSet.prototype.delete(value)  清除 WeakSet 实例的指定成员。
	WeakSet.prototype.has(value)     返回一个布尔值，表示某个值是否在 WeakSet 实例之中
  // WeakSet 没有size属性，没有办法遍历它的成员
  #

[Map]

	# JS对象, 本质上是键值对的集合(Hash 结构), 但是传统上只能用字符串当作键
  // 构造函数
  
  # 属性
  size  返回 Map 结构的成员总数
  Map.prototype.set(key, value)  设置键名key对应的键值为value，然后返回整个 Map 结构
  Map.prototype.get(key)  读取key对应的键值，如果找不到key，返回undefined
  Map.prototype.has(key)  某个键是否在当前 Map 对象之中
  Map.prototype.delete(key) 删除某个键，返回true。如果删除失败，返回false
  Map.prototype.clear()  清除所有成员
  // - 遍历方法
  Map.prototype.keys()    返回键名的遍历器
	Map.prototype.values()  返回键值的遍历器
	Map.prototype.entries() 返回所有成员的遍历器
	Map.prototype.forEach() 遍历 Map 的所有成员
  // Map 的遍历顺序就是插入顺序
  // Map 结构转为数组结构，比较快速的方法是使用扩展运算符（...）

[WeakMap]

	# WeakMap结构与Map结构类似，也是用于生成键值对的集合
  // WeakMap只接受对象作为键名（null除外），不接受其他类型的值作为键名
  // WeakMap的键名所指向的对象，不计入垃圾回收机制
  
```

### Proxy (拦截器)

```
[]

	# 用于修改某些操作的默认行为, 等同于在语言层面做出修改
  // 属于 “元编程” (meta programming), 即对编程语言进行编程
  // 拦截机制, 外界对该对象的访问, 都必须先通过这层拦截, 这样可以对外界的访问进行过滤和改写
  
  # 重载(overload)了点运算符, 即用自己的定义覆盖了语言的原始定义
  // var proxy = new Proxy(target, handler);

// 重定义了属性的读取(get)和设置(set)行为
// 赋值 : obj.count = 1
// 取值 : var a = obj.count
// 
var obj = new Proxy({}, {
  get: function (target, key, receiver) {
    console.log(`getting ${key}!`);
    return Reflect.get(target, key, receiver);
  },
  set: function (target, key, value, receiver) {
    console.log(`setting ${key}!`);
    return Reflect.set(target, key, value, receiver);
  }
});

	# 实例方法(拦截操作) (13个)
  get(target, propKey, receiver)  拦截对象属性的读取, 比如proxy.foo和proxy['foo']。
	set(target, propKey, value, receiver) 拦截对象属性的设置, 比如proxy.foo = v或proxy['foo'] = v，返回一个布尔值。
	has(target, propKey) 拦截propKey in proxy的操作, 返回一个布尔值
	deleteProperty(target, propKey) 拦截delete proxy[propKey]的操作，返回一个布尔值。
	ownKeys(target) 拦截Object.getOwnPropertyNames(proxy)、Object.getOwnPropertySymbols(proxy)、Object.keys(proxy)、for...in循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而Object.keys()的返回结果仅包括目标对象自身的可遍历属性。
	getOwnPropertyDescriptor(target, propKey) 拦截Object.getOwnPropertyDescriptor(proxy, propKey)，返回属性的描述对象。
	defineProperty(target, propKey, propDesc) 拦截Object.defineProperty(proxy, propKey, propDesc）、Object.defineProperties(proxy, propDescs)，返回一个布尔值。
	preventExtensions(target) 拦截Object.preventExtensions(proxy)，返回一个布尔值。
	getPrototypeOf(target) 拦截Object.getPrototypeOf(proxy)，返回一个对象。
	isExtensible(target) 拦截Object.isExtensible(proxy)，返回一个布尔值。
	setPrototypeOf(target, proto) 拦截Object.setPrototypeOf(proxy, proto)，返回一个布尔值。如果目标对象是函数，那么还有两种额外操作可以拦截。
	apply(target, object, args) 拦截 Proxy 实例作为函数调用的操作，比如proxy(...args)、proxy.call(object, ...args)、proxy.apply(...)。
	construct(target, args) 拦截 Proxy 实例作为构造函数调用的操作，比如new proxy(...args)

```

### Reflect

```
[]

	#  ES6 为了操作对象而提供的新 API
  // - 将Object对象的一些明显属于语言内部的方法, 放到Reflect对象上
  // - 修改某些Object方法的返回结果，让其变得更合理
  // - 让Object操作都变成函数行为
  // - Reflect与Proxy对象的方法一一对应
  
  # 静态方法
  Reflect.apply(target, thisArg, args)
	Reflect.construct(target, args)
	Reflect.get(target, name, receiver)
	Reflect.set(target, name, value, receiver)
	Reflect.defineProperty(target, name, desc)
	Reflect.deleteProperty(target, name)
	Reflect.has(target, name)
	Reflect.ownKeys(target)
	Reflect.isExtensible(target)
	Reflect.preventExtensions(target)
	Reflect.getOwnPropertyDescriptor(target, name)
	Reflect.getPrototypeOf(target)
	Reflect.setPrototypeOf(target, prototype)
  
  # 解析

```

### Promise (回调异步-语法糖)

```javascript
[Promise (ES6)]

	# JS 异步操作解决方案, 为异步操作提供统一接口
  // Promise 简单说就是一个容器, 里面保存着某个未来才会结束的事件(通常是一个异步操作)的结果
  // 代理作用 (proxy), 充当异步操作与回调函数之间的中介, 使得异步操作具备同步操作的接口
  // 可以让异步操作写起来, 就像在写同步操作的流程, 而不必一层层地嵌套回调函数
  
  # 构造函数, 接受一个回调函数作为参数
  // 设计思想是, 所有异步任务都返回一个Promise实例
  // 传统的回调函数写法使得代码混成一团，变得横向发展而不是向下发展
  // 优点在于, 让回调函数变成了规范的链式写法, 程序流程可以看得很清楚
  // 缺点是，编写的难度比传统写法高，而且阅读代码也不是一眼可以看懂

  # 对象状态
  // 对象的状态不受外界影响, 只有异步操作的结果, 可以决定当前是哪一种状态, 一旦状态改变就不再变
  // - 异步操作未完成 pending
  // - 异步操作成功   fulfilled
  // - 异步操作失败   rejected  (fulfilled和rejected合在一起称为 resolved (已定型))
  // 异步操作成功, Promise 实例传回一个值 (value), 状态变为fulfilled
  // 异步操作失败, Promise 实例抛出一个错误 (error), 状态变为rejected
  
  # 缺点
  // 无法取消Promise, 一旦新建它就会立即执行, 无法中途取消
  // 如果不设置回调函数,Promise内部抛出的错误,不会反应到外部
  // 当处于pending状态时, 无法得知目前进展到哪一个阶段
  
  // Promise 的回调函数不是正常的异步任务, 而是微任务(microtask)
  // 它们的区别在于, 正常任务追加到下一轮事件循环, 微任务追加到本轮事件循环
  
  # 实例方法
  Promise.prototype.then()  实例添加状态改变时的回调函数,指定下一步的回调函数, 返回一个新的Promise实例
  // 指定resolved状态和rejected状态的回调函数
	Promise.prototype.catch() 用于指定发生错误时的回调函数
	// .then(null, rejection) 或.then(undefined, rejection)的别名
  // 如果异步操作抛出错误，状态就会变为rejected，就会调用catch方法指定的回调函数，处理这个错误
  // then方法指定的回调函数，如果运行中抛出错误，也会被catch方法捕获
  // Promise 对象的错误具有“冒泡”性质，会一直向后传递，直到被捕获为止
  // 如果没有使用catch方法指定错误处理的回调函数，Promise 对象抛出的错误不会传递到外层代码，即不会有任何反应
	// catch方法返回的还是一个 Promise 对象，因此后面还可以接着调用then方法
  Promise.prototype.finally() 指定不管 Promise 对象最后状态如何，都会执行的操作(ES2018 引入标准)
	// finally方法的回调函数不接受任何参数, 操作，应该是与状态无关的，不依赖于 Promise 的执行结果
	// finally本质上是then方法的特例, 成功错误处理代码一致
	Promise.all()
  Promise.race()
	Promise.allSettled()
	Promise.any()
	Promise.resolve()
	Promise.reject()
	Promise.try()

```

### Iterator (遍历器) 

```javascript
[]

	# 
  // 任何数据结构只要部署 Iterator 接口, 就可以完成遍历操作 (即依次处理该数据结构的所有成员)
  // - 为各种数据结构，提供一个统一的、简便的访问接口
  // - 使得数据结构的成员能够按某种次序排列
  // - ES6 创造了一种新的遍历命令for...of循环，Iterator 接口主要供 for...of消费
  // ES6 规定, 默认的 Iterator 接口部署在数据结构的Symbol.iterator属性
  // 
  
  # 表示数据集合的数据结构
  // 数组 Array
  // 对象 Object
  // Map
  // Set
  // - 遍历器, 统一的接口机制, 来处理所有不同的数据结构
  
  # 遍历过程 next()
  // - 创建一个指针对象，指向当前数据结构的起始位置 (遍历器对象本质上, 就是一个指针对象)
  // - 调用指针对象的next方法, 可以将指针指向数据结构的第一个成员
  // - 调用指针对象的next方法, 指针就指向数据结构的第二个成员
  // - 不断调用指针对象的next方法, 直到它指向数据结构的结束位置
  // 返回数据结构的当前成员信息的对象 (属性: value 当前成员的值 和done 布尔值, 表示遍历是否结束)
  
  # 调用 Iterator 接口的场合
  // 解构赋值
  // 扩展运算符
  // yield*
  // 其他场合

  # return()
  // return方法的使用场合是, 如果for...of循环提前退出, 就会调用return方法
  // 如果一个对象在完成遍历前, 需要清理或释放资源, 就可以部署return方法
  // return方法必须返回一个对象，这是 Generator 规格决定

  # throw()
  // throw方法主要是配合 Generator 函数使用，一般的遍历器对象用不到这个方法

```

### Generator (异步执行)

```javascript
[]

	# ES6 提供的一种异步编程解决方案, 语法行为与传统函数完全不同
  // 语法上, Generator 函数是一个状态机, 封装了多个内部状态, 返回遍历器对象
  // 星号声明函数, 函数体内部使用yield表达式 定义不同的内部状态
  // 定义 : function* generator() {}
	// - 调用后并不执行, 仅返回一个指向内部状态的指针对象, 即遍历器对象 (Iterator Object)
  // - 调用遍历器对象的next方法, 使得指针移向下一个状态
  // Generator 函数分段执行的, yield表达式是暂停执行的标记, 而next方法可以恢复执行
  
  # yield 表达式
  // 只能用在 Generator 函数里面
  // yield表达式本身没有返回值，或者说总是返回undefined
  // yield命令, 表示执行到此处, 执行权将交给其他协程, yield命令是异步两个阶段的分界线
  
  # next
  // 可以带一个参数, 该参数就会被当作上一个yield表达式的返回值
  // Generator 函数从暂停状态到恢复运行, 它的上下文状态（context）是不变的
  // 通过next方法的参数, 就有办法在 Generator 函数开始运行之后, 继续向函数体内部注入值

	#
 	Generator.prototype.throw()
	// 在函数体外抛出错误, 然后在 Generator 函数体内捕获
	Generator.prototype.return()
	// 返回给定的值, 并且终结遍历 Generator 函数

	# next()、throw()、return()
  // 本质上是同一件事, 作用都是让 Generator 函数恢复执行, 并且使用不同的语句替换yield表达式
  // next()是将yield表达式替换成一个值
  // throw()是将yield表达式替换成一个throw语句
  // return()是将yield表达式替换成一个return语句
  
  # yield* 表达式
  // Generator 函数内部, 调用另一个 Generator 函数, 需要手动完成遍历执行后者
  // ES6 yield* 表达式 , 用来在一个 Generator 函数里面执行另一个 Generator 函数
  
  # 异步编程方式
  // - 回调函数  (任务第二段单独写在一个函数里面, 等到重新执行这个任务的时候, 就直接调用这个函数)
  // - 事件监听
  // - 发布/订阅
  // - Promise 对象 (解决回调函数嵌套问题, callback hell | 不是新语法而是回调函数新写法)
  // - Generator 函数 (协程)
  
  # Thunk
  // 自动执行 Generator 函数的一种方法
```

### Async (异步执行-语法糖)

```javascript
[async 函数]

	# ES2017 标准引入了 async 函数, 使得异步操作变得更加方便
  // 简单说其就是 Generator 函数的语法糖
  
  # 语法
  // async function () { await fun() }
  // async函数, 就是将 Generator 函数的星号(*)替换成 async, 将yield替换成await
  
  # 改进
  // 内置执行器, Generator 函数的执行必须靠执行器, 所以才有了co模块, 而async函数自带执行器
  // 更好的语义 , sync和await, 比起星号和yield, 语义更清楚
  // 更广的适用性
  // 返回值是 Promise (Generator 函数的返回值是 Iterator)
  // async函数完全可以看作多个异步操作, 包装成的一个 Promise 对象, 而await命令就是内部then命令的语法糖

```

### ArrayBuffer

```
[二进制数据操作接口]

	# 
  // 属于独立的规格(2011 年 2 月发布), ES6 将它们纳入了 ECMAScript 规格, 并且增加了新的方法
  // 以数组的语法处理二进制数据, 所以统称为二进制数组
  // 二进制数组并不是真正的数组, 而是类似数组的对象

	# ArrayBuffer 对象
  // 代表储存二进制数据的一段内存, 它不能直接读写, 只能通过视图操作读写
  // 视图的作用是以指定格式解读二进制数据
  // 构造函数, 可以分配一段可以存放数据的连续内存区域
  
  ArrayBuffer.prototype.byteLength  返回所分配的内存区域的字节长度
  ArrayBuffer.prototype.slice() 允许将内存区域的一部分, 拷贝生成一个新的ArrayBuffer对象
  ArrayBuffer.isView() 静态方法, 判断参数是否为TypedArray实例或DataView实例
  
  # TypedArray视图
  // 9 种类型的视图
  // 视图还可以不通过ArrayBuffer对象, 直接分配内存而生成
  // 普通数组的操作方法和属性, 对 TypedArray 数组完全适用
  
  TypedArray.prototype.buffer 返回整段内存区域对应的ArrayBuffer对象 (只读)
  TypedArray.prototype.byteLength 返回 TypedArray 数组占据的内存长度, 单位为字节
  TypedArray.prototype.byteOffset 返回 TypedArray 数组从底层ArrayBuffer对象的哪个字节开始
  TypedArray.prototype.length 表示 TypedArray 数组含有多少个成员
  TypedArray.prototype.set() 用于复制数组（普通数组或 TypedArray 数组）
  TypedArray.prototype.subarray()  对于 TypedArray 数组的一部分，再建立一个新的视图
  TypedArray.prototype.slice() 返回一个指定位置的新的TypedArray实例
  TypedArray.of() 静态方法 用于将参数转为一个TypedArray实例
  TypedArray.from() 静态方法 返回一个基于这个结构的TypedArray实例

  # DataView视图
  // 自定义复合格式的视图, 支持除Uint8C以外的其他8种
  
  DataView.prototype.buffer：返回对应的 ArrayBuffer 对象
	DataView.prototype.byteLength：返回占据的内存字节长度
	DataView.prototype.byteOffset：返回当前视图从对应的 ArrayBuffer 对象的哪个字节开始

  DataView.prototype.getInt8   读取 1 个字节，返回一个 8 位整数
  DataView.prototype.getUint8  读取 1 个字节，返回一个无符号的 8 位整数
  DataView.prototype.getInt16  读取 2 个字节，返回一个 16 位整数
  DataView.prototype.getUint16 读取 2 个字节，返回一个无符号的 16 位整数
  DataView.prototype.getInt32  读取 4 个字节，返回一个 32 位整数
  DataView.prototype.getUint32 读取 4 个字节，返回一个无符号的 32 位整数
  DataView.prototype.getFloat32 读取 4 个字节，返回一个 32 位浮点数
  DataView.prototype.getFloat64 读取 8 个字节，返回一个 64 位浮点数
  
  DataView.prototype.setInt8   写入 1 个字节的 8 位整数
  DataView.prototype.setUint8  写入 1 个字节的 8 位无符号整数
  DataView.prototype.setInt16  写入 2 个字节的 16 位整数
  DataView.prototype.setUint16 写入 2 个字节的 16 位无符号整数
  DataView.prototype.setInt32  写入 4 个字节的 32 位整数
  DataView.prototype.setUint32 写入 4 个字节的 32 位无符号整数
  DataView.prototype.setFloat32  写入 4 个字节的 32 位浮点数
  DataView.prototype.setFloat64  写入 8 个字节的 64 位浮点数

  
  # 字节序
  // 数值在内存中的表示方式
  //  x86 体系的计算机都采用小端字节序 (little endian)
  
  BYTES_PER_ELEMENT 属性, 表示这种数据类型占据的字节数 (视图的构造函数)
  TypedArray.prototype.BYTES_PER_ELEMENT
  
  # ArrayBuffer 与字符串的互相转换 -> TextEncoder TextDecoder
  
  # 溢出, 超出视图能表示的范围
  // TypedArray 数组的溢出处理规则, 简单来说, 就是抛弃溢出的位, 然后按照视图类型进行解释
  // 负数在计算机内部采用“2 的补码”表示

[SharedArrayBuffer]

	# ES2017 引入, 允许 Worker 线程与主线程共享同一块内存
  // Web worker 引入了多线程

[Atomics 对象]

	# 保证所有共享内存的操作都是“原子性”的, 并且可以在所有线程内同步。
	// SharedArrayBuffer API 提供Atomics对象

  Atomics.store() 向共享内存写入数据 , 返回写入的值
  Atomics.load()  从共享内存读出数据
  Atomics.exchange() 向共享内存写入数据 , 返回被替换的值
  Atomics.wait()  用于等待通知, 等待主线程的通知，不是很高效
  Atomics.wake()  用于等待通知, 
	

[操作]

// 定义32字节内存, 二进制数组 (初始化为 0)
const buf = new ArrayBuffer(32);

// 指定视图
const dataView = new DataView(buf);

// 以不带符号的 8 位整数格式, 从头读取 8 位二进制数据
dataView.getUint8(0) 

// TypedArray - 一组构造函数, 代表不同的数据格式
const dataView = new Int32Array(buf);
//
dataView[0] = 1;

```

九种基本视图

| 数据类型 | 字节长度 | 含义 | 对应的 C 语言类型 |
| --- | --- | --- | --- |
| Int8 | 1 | 8 位带符号整数 | signed char |
| Uint8 | 1 | 8 位不带符号整数 | unsigned char |
| Uint8C | 1 | 8 位不带符号整数（自动过滤溢出） | unsigned char |
| Int16 | 2 | 16 位带符号整数 | short |
| Uint16 | 2 | 16 位不带符号整数 | unsigned short |
| Int32 | 4 | 32 位带符号整数 | int |
| Uint32 | 4 | 32 位不带符号的整数 | unsigned int |
| Float32 | 4 | 32 位浮点数 | float |
| Float64 | 8 | 64 位浮点数 | double |

