### Class 类

```javascript
[class]

	# js 生成实例对象的传统方法是通过构造函数
  // ES6 提供了和传统创建类实例一样的写法 Class , 作为对象的模板, 通过class创建类
  // 本质上, class 是构造函数写法的语法糖, 只是让对象原型的写法更加清晰、更像面向对象编程的语法
  // 类和模块的内部, 默认就是严格模式
  // 类不存在变量提升 (hoist)
  // 类的方法内部如果含有this, 它默认指向类的实例 (箭头函数内部的this总是指向定义时所在的对象)
  # 
  // 类的内部所有定义的方法, 都是不可枚举的 (non-enumerable)
  // 类必须使用new调用, 否则会报错
  // 实例的属性除非显式定义在其本身(即定义在this对象上), 否则都是定义在原型上(即定义在class上)
  
  # constructor 方法
  // 类默认方法, 没有显式定义, 一个空的constructor方法会被默认添加
  
  # 取值函数(getter)和存值函数(setter)
  // 对某个属性设置存值函数和取值函数, 拦截该属性的存取行为
  
  # 静态方法 (static 关键字)
  // 静态方法包含this关键字, 这个this指的是类, 而不是实例
  // 静态方法可以与非静态方法重名
  // 父类的静态方法，可以被子类继承

  # 静态属性 (Class 本身的属性)
  // ES6 明确规定，Class 内部只有静态方法, 没有静态属性
  
  # 私有方法和私有属性
  // 定义再类外部
  // 只能在类的内部访问的方法和属性，外部不能访问 (ES6 不提供，只能通过变通方法模拟实现)
  // - 提案, 为class加了私有属性, 方法是在属性名之前，使用#表示。
  
  # new.target 属性
  // ES6  new.target属性, 该属性一般用在构造函数之中, 返回new命令作用于的那个构造函数
  // 构造函数不是通过new命令或Reflect.construct()调用的，new.target会返回undefined
  // 子类继承父类时，new.target会返回子类

[extends 继承]

	# extends定义 继承, 这比 ES5 的通过修改原型链实现继承, 要清晰和方便很多
  // 继承了父类的所有属性和方法
  // 子类必须在constructor方法中调用super方法, 否则新建实例时会报错
  // ES5继承, 实质是先创造子类的实例对象this, 然后再将父类的方法添加到this上面(Parent.apply(this))
  // ES6则完全不同, 实质是先将父类实例对象的属性和方法加到this上面, 然后再用子类的构造函数修改this
	// 子类的构造函数中, 只有调用super之后, 才可以使用this关键字
  // 父类的静态方法, 也会被子类继承

	# super
  // 既可以当作函数使用，也可以当作对象使用
  // 作为函数, 代表父类的构造函数, ES6 要求, 子类的构造函数必须执行一次super函数
  A.prototype.constructor.call(this) # super虽然代表了父类A的构造函数，但是返回的是子类B的实例
  // 作为函数时，super()只能用在子类的构造函数之中，用在其他地方就会报错
	// super作为对象时, 在普通方法中, 指向父类的原型对象, 在静态方法中, 指向父类
  // super指向父类的原型对象, 所以定义在父类实例上的方法或属性, 是无法通过super调用
  super.print.call(this) # 执行的方法中的this 绑定在当前子类对象
	// 
  
  # 类的 prototype 属性和__proto__属性
  // Class 作为构造函数的语法糖，同时有prototype属性和__proto__属性，因此同时存在两条继承链
  // 子类的__proto__属性, 表示构造函数的继承, 总是指向父类
  // 子类prototype属性的__proto__属性, 表示方法的继承, 总是指向父类的prototype属性
  // - ES5 实现之中，每一个对象都有__proto__属性，指向对应的构造函数的prototype属性
  
  Object.getPrototypeOf() 用来从子类上获取父类

[Mixin 模式]

	# 指的是多个对象合成一个新的对象, 新对象具有各个组成成员的接口
```

```javascript
[构造函数生成对象]

// 定义构造函数 (this 定义实例属性, 不含this 则定义没有属性的空对象)
function Point(x, y) {
  this.x = x;
  this.y = y;
}

// 定义原型方法
Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

// new 调用构造函数, 生成实例对象
var p = new Point(1, 2);

[Class 语法生成对象]

// 定义类 (构造函数的另一种写法)
class Point {
  // 定义构造函数
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  // 定义实例方法
  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}

// new 调用类(构造函数), 生成实例对象
var p = new Point(1, 2);

[继承模式]

class A {}

class B {}

// B 的实例继承 A 的实例
Object.setPrototypeOf(B.prototype, A.prototype);

// B 继承 A 的静态属性
Object.setPrototypeOf(B, A);

const b = new B();

[Mixin 模式]

// 简单实现
const a = {
  a: 'a'
};
const b = {
  b: 'b'
};

const c = {...a, ...b}; //

// 多个类的接口混入 (mix in)另一个类, 将多个对象合成为一个类
function mix(...mixins) {
  class Mix {
    constructor() {
      for (let mixin of mixins) {
        copyProperties(this, new mixin()); // 拷贝实例属性
      }
    }
  }

  for (let mixin of mixins) {
    copyProperties(Mix, mixin); // 拷贝静态属性
    copyProperties(Mix.prototype, mixin.prototype); // 拷贝原型属性
  }

  return Mix;
}

function copyProperties(target, source) {
  for (let key of Reflect.ownKeys(source)) {
    if ( key !== 'constructor'
      && key !== 'prototype'
      && key !== 'name'
    ) {
      let desc = Object.getOwnPropertyDescriptor(source, key);
      Object.defineProperty(target, key, desc);
    }
  }
}

class DistributedEdit extends mix(Loggable, Serializable) {
  // ...
}
```

### Module

```javascript
[mudule]

	# 
  // js一直没有模块体系, 无法将一个大程序拆分成互相依赖的小文件, 再用简单的方法拼装起来
  // 社区制定了一些模块加载方案, 最主要的有 CommonJS (服务器) 和 AMD(浏览器) 两种
	// ES6 实现了模块功能, 而且实现得相当简单, 完全可以取代 CommonJS 和 AMD 规范
  // ES6 模块的设计思想是尽量的静态化,使得编译时就能确定模块的依赖关系，以及输入和输出的变量
  
  # require
  // 整体加载, 运行时加载
  
  # 模块
  // 加载指定方法, 编译时加载
  // 编译时加载 - 静态分析 - 引入宏(macro)和类型检验(type system)
  // 严格模式
  //
  
  # export
  // 用于规定模块的对外接口
  // 一个模块就是一个独立的文件, 文件内部的所有变量，外部无法获取
  // 外部访问则必须 export 显示声明导出
  // export语句输出的接口, 与其对应的值是动态绑定关系, 即通过该接口, 可以取到模块内部实时的值
  // export default , 模块指定默认输出
  
  # import
  // 用于输入其他模块提供的功能
  // import ... from '...';
  // 模块的整体加载 import * as obj from '...' // 不允许运行时改变
  
  # 复合写法, 先输入后输出同一个模块
  // export { a, b } from '...' // 实际上并没有被导入当前模块, 只是相当于对外转发了这两个接口
	// export * from '..'; // 导出所有, 相当于模块继承
  
  # 运行时加载
  // import()  # 提案

[模块加载方案]

	# 浏览器加载
  // 浏览器加载, 通过<script>标签加载 JavaScript 脚本
  <script src="path/to/myModule.js" defer></script> // 异步加载方案
	<script src="path/to/myModule.js" async></script> // 异步加载方案
	// defer要等到整个页面在内存中正常渲染结束, 才会执行, async 下载完成就中断渲染并执行

	# 浏览器加载 ES6 模块, 加载规则
  // 也使用<script>标签，但是要加入type="module"属性
  <script type="module" src="./foo.js"></script>
	// 异步加载,整个页面渲染完，再执行模块脚本
  // 对于外部的模块脚本
	// - 代码是在模块作用域之中运行,, 而不是在全局作用域运行, 模块内部的顶层变量, 外部不可见
	// - 模块脚本自动采用严格模式, 不管有没有声明use strict
	// - 模块之中, 可以使用import命令加载其他模块 (js后缀不可省略), 可以使用export命令输出对外接口
	// - 模块之中, 顶层的this关键字返回undefined, 而不是指向window
	// - 同一个模块如果加载多次, 将只执行一次

```

