
```
[对象属性模型的相关方法]

	# 获取某个属性的描述对象
	: Object.getOwnPropertyDescriptor()

	# 通过描述对象，定义某个属性
	: Object.defineProperty()

	# 通过描述对象, 定义多个属性
	: Object.defineProperties()
```

Object的defineProperty和defineProperties这两个方法在js中的重要性十分重要，主要功能就是用来定义或修改这些内部属性,与之相对应的getOwnPropertyDescriptor和getOwnPropertyDescriptors就是获取这行内部属性的描述。

ECMAS-262第5版在定义只有内部采用的特性时，提供了描述了属性特征的几种属性。ECMAScript对象中目前存在的属性描述符主要有两种，数据描述符(数据属性)和存取描述符(访问器属性)，数据描述符是一个拥有可写或不可写值的属性。存取描述符是由一对 getter-setter 函数功能来描述的属性。

```
[Object.defineProperty()]

	: 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象。

  : https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineproperty

[语法]

	: Object.defineProperty(obj, prop, descriptor)

  : 参数
  # obj        要在其上定义属性的对象
	# prop       要定义或修改的属性的名称
	# descriptor 将被定义或修改的属性描述符

  : 返回值
  # 被传递给函数的对象

  : 该方法允许精确添加或修改对象的属性。通过赋值操作添加的普通属性是可枚举的, 
  能够在属性枚举期间呈现出来（for...in 或 Object.keys 方法）, 这些属性的值可以被改变或被删除。
  这个方法允许修改默认的额外选项（或配置）。
  默认情况下，使用 Object.defineProperty() 添加的属性值是不可修改的。

[属性描述符]

	: 对象里目前存在的属性描述符有两种主要形式：数据描述符和存取描述符。

  # 数据描述符是一个具有值的属性，该值可能是可写的，也可能不是可写的。
  # 存取描述符是由getter-setter函数对描述的属性。描述符必须是这两种形式之一；不能同时是两者。

	: 数据描述符同时具有以下可选键值
  # value  该属性对应的值。可以是任何有效的 JavaScript 值, 默认为 undefined。
  # writable 当且仅当该属性的writable为true时，value才能被赋值运算符改变。默认为 false。

	: 存取描述符同时具有以下可选键值
  # get  一个给属性提供 getter 的方法, 当访问该属性时, 该方法会被执行, 默认为 undefined
  # set  一个给属性提供 setter 的方法, 当属性值修改时，触发执行该方法, 默认为 undefined

  : 数据描述符和存取描述符均具有以下可选键值
  # configurable 当且仅当该属性的 configurable 为 true 时，该属性描述符才能够被改变，同时该属性也能从对应的对象上被删除。默认为 false。
  # enumerable   当且仅当该属性的enumerable为true时，该属性才能够出现在对象的枚举属性中。默认为 false。

// 如果一个描述符不具有value,writable,get 和 set 任意一个关键字，那么它将被认为是一个数据描述符。如果一个描述符同时有(value或writable)和(get或set)关键字，将会产生一个异常。
```

### 实现案例

```javascript
// A、使用 __proto__
var obj = {};

// B、数据(数据描述符)属性

// 01 定义描述符 [默认没有 enumerable, 没有 configurable, 没有 writable]
var descriptor = Object.create(null); // 没有继承的属性
// 02 描述符添加值
descriptor.value = 'v';
// 03 为对象 obj , 添加 key 为 k , 值为 v 的属性  { k:v }
Object.defineProperty(obj, 'k', descriptor);

// 01 显式定义, 属性描述符号, 并为对象 obj , 添加属性 { k1:v1 }
Object.defineProperty(obj, "k1", {
    enumerable: false,
    configurable: false,
    writable: false,
    value: "v1"
});

// 获取 obj 对象, k 属性的描述符信息
var kd = Object.getOwnPropertyDescriptor(obj, 'k')

// C、访问器(存取描述符)属性

// 定义内部数据, 存放 存储操作符属性的值 (使用此方法可以对外部数据, 进行代理监控其取值和赋值操作)
var _data = {};

//
Object.defineProperty(obj, "k2", {
    get: function () {
        console.log('get xxx')
        return _data.k2
    },
    set: function (v) {
        console.log('set xxx')
        _data.k2 = v
    }
});

// obj.k2 = 'value' , 赋值操作时, 触发 set 执行
// obj.k2             取值操作时, 触发 get 执行
```

![](http://localhost/it/front-end/1574088648735-1ea1d759-9722-4ff9-a8fa-b16afd4d5b0f.webp#align=left&display=inline&height=1114&originHeight=1114&originWidth=1224&size=0&status=done&width=1224)
