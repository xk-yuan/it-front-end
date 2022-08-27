```javascript
[]

	# 编程范式, 将各种复杂的关系, 抽象为对象, 由对象之间的分工与合作, 完成业务逻辑

  # 过程式编程 Procedural Programming
  // 一系列函数或指令组成

  # 对象 Object
  // - 对象是单个实物的抽象
	// - 对象是一个容器，封装了属性(property)和方法(method) (属性是对象的状态，方法是对象的行为)

  # 构造函数
  // 面向对象编程的第一步, 就是要生成对象, 其需要一个模板, 表示某一类实物的共同特征
  // JS 对象体系, 不是基于“类”的, 而是基于构造函数(constructor)和原型链(prototype)
  // JS 使用构造函数作为对象的模板, 构造函数就是一个普通的函数, 但是有自己的特征和用法
  // 构造函数名字的第一个字母通常大写
  // - 函数体内部使用了this关键字, 代表了所要生成的对象实例
  // - 生成对象的时候, 必须使用new命令

  # new
  // 该命令, 作用是执行构造函数, 返回一个实例对象
  // 执行步骤
  // - 创建一个空对象，作为将要返回的对象实例
  // - 将这个空对象的原型，指向构造函数的prototype属性
  // - 将这个空对象赋值给函数内部的this关键字
  // - 开始执行构造函数内部的代码
  // new.target , 当前函数是new命令调用, new.target指向当前函数, 否则为undefined
  Object.create() 以这个现有的对象作为模板，生成新的实例对

[this]

	# this 可以用在构造函数之中, 表示实例对象, 其总是返回一个对象 (就是属性或方法“当前”所在的对象)
  // 由于对象的属性可以赋给另一个对象, 所以属性所在的当前对象是可变的, 即this的指向是可变的

  # 使用场合
  // 全局环境, 指的就是顶层对象window
  // 构造函数, 指的是实例对象
  // 对象的方法, 指向就是方法运行时所在的对象
  // - 如果this所在的方法不在对象的第一层，这时this只是指向当前一层的对象，而不会继承更上面的层
  // - 避免多层 this (第二层改用一个指向外层this的变量)

  # 绑定 this
  Function.prototype.call() 指定函数内部this的指向(执行时所在作用域), 然后在所指定的作用域中执行
	// 其调用对象的原生方法 (如果方法被覆盖)
	Function.prototype.apply() 功能和 call 方法一致, 区别是接收一个数组作为函数执行时的参数
	Function.prototype.bind()  将函数体内的this绑定到某个对象, 然后返回一个新函数

[prototype]

	# 面向对象编程很重要的一个方面，就是对象的继承 (JS 使用原型对象(prototype), 实现继承)
  // 继承机制的设计思想就是, 原型对象的所有属性和方法, 都能被实例对象共享
  // 定义所有实例对象共享的属性和方法
  // JS 构造函数生成新对象, 因此构造函数可以视为对象的模板
  // 实例对象的属性和方法, 可以定义在构造函数内部
  // 缺点是, 同一个构造函数的多个实例之间, 无法共享属性, 从而造成对系统资源的浪费
  
  # 原型链
  // Object.prototype
  
  # constructor 属性
  // 默认指向prototype对象所在的构造函数
  // 作用是，可以得知某个实例对象，到底是哪一个构造函数产生的
  // 表示原型对象与构造函数之间的关联关系, 如果修改了原型对象, 一般会同时修改constructor属性
  
  instanceof 表示对象是否为某个构造函数的实例
	Object.isPrototypeOf()
  

[Object]

	# 
  Object.getPrototypeOf() 返回参数对象的原型
  Object.setPrototypeOf() 参数对象设置原型，返回该参数对象
  Object.create()
  // Object.create(null)  创建的空对象的原型是 null, 且没有构造函数
	Object.getOwnPropertyNames() 获取对象所有非继承的属性键名
  Object.getOwnPropertyDescriptors() // ES2017
 
	#
  Object.prototype.isPrototypeOf() 判断该对象是否为参数对象的原型
  Object.prototype.__proto__ 返回该对象的原型
  Object.prototype.hasOwnProperty() 判断某个属性定义在对象自身，还是定义在原型链上
  
  
  # in 运算符和 for…in 循环
  in 运算符返回一个布尔值, 表示一个对象是否具有某个属性, 不区分是否继承

	# 对象的拷贝
  // 确保拷贝后的对象，与原对象具有同样的原型
  // 确保拷贝后的对象，与原对象具有同样的实例属性

[面向对象编程的模式]

	# Mixin (混入) - 多重继承
  Object.assign() 添加继承链

  # 封装私有变量：立即执行函数的写法
var module1 = (function () {
　var _count = 0;
　var m1 = function () {
　};
　return {
　　m1 : m1
　};
})();
  // - 放大模式 augmentation
var module1 = (function (mod){
  // module1 添加方法 m2
　mod.m2 = function () {
　};
　return mod;
})(module1);
	// 宽放大模式 Loose augmentation
var module1 = ( function (mod){
　//...
　return mod;
})(window.module1 || {});

```

### 模拟 New 函数创建对象

```javascript
/**
 * 模拟 new 创建对象
 * 
 * @param {*} constructor 构造函数
 * @param {*} params      参数
 */
function _new(constructor, params) {
    // 将 arguments 对象转为数组
    var args = [].slice.call(arguments);
    // 取出构造函数
    var constructor = args.shift();
    // 创建一个空对象, 继承构造函数的 prototype 属性
    var context = Object.create(constructor.prototype);

    // 执行构造函数
    var result = constructor.apply(context, args);
    // 如果返回结果是对象 (构造函数中, 有可能返回对象), 就直接返回, 否则返回 context 对象
    return (typeof result === 'object' && result != null) ? result : context;
}

// 定义构造函数 (普通函数)
function Person() {

}

// 实例
var actor = _new(Person, '张三', 1);

```

```javascript
[定义父类]

function Base() {}

[子类继承]

var b = new Base()

// 通过 Object.create() 创建的子类对象, 和父类对象是强耦合的, 父类属性改变 在所有子类可以查看
// Base.属性 + Sub.__proto__.属性
// 子类对父类相同属性名的修改, 只有该子类可以访问, 此时该属性名为直接定义在该对象实例上面
// Sub.属性 + Sub.__proto__.属性
var s = Object.create(b)

// 此时内存对象状态

	: b => Base{ _proto_: {constructor: Base(), _proto_: Object}}

[解析]

	: 继承, 通过 _proto_ 属性进行关联
  
  : 子类使用属性和方法时, 先查询自身, 查询不到通过 _proto_ 原型链进行溯源查询

[原型属性 - prototype]

	: __proto__
```

![image.png](http://localhost/it/front-end/1574123125245-e2e265c6-4240-465a-9f5e-7453417365f5.png#align=left&display=inline&height=725&name=image.png&originHeight=583&originWidth=600&size=74242&status=done&style=none&width=746)
