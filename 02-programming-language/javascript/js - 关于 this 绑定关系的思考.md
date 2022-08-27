几段代码 this 绑定关系

```
// 代码段 一
function Person(){
  console.log(this)
  setInterval(function func() {
    console.log(this)
  }, 3000);
}

// 执行方式 一
Person()

// 指向方式 二 , 第一次 初始化时 this 指向 Person , 其后执行 指向 window
new Person()
```

```
// 代码段 二
function Person(){
  var selt = this;
  setInterval(function a() {
    console.log(selt)
  }, 1000);
}

// 执行方式 一 | this 指向 window
Person()

// 指向方式 二 | this 指向 Person
new Person()


// 代码段三 | 匿名函数
function Person(){
  setInterval(() => {
    console.log(this)
  }, 1000);
}

// 执行方式 一 | this 指向 window


// 指向方式 二 | this 指向 Person
new Person()
```

```
[结论]

	: Person() 直接执行时, 以window对象执行函数
  
  : new Person() 创建一个Person对象, 以该对象身份执行函数

[]

function Person(){
  // this 创建时为全局变量域, 调用函数时不会自动切换this绑定对象
  // 但当在该域声明变量时, var self 将该变量声明到 Person 域中, this 将根据变量声明进行切换
}

// 声明匿名函数时, 将会自动切换 this 绑定当前对象中
```

