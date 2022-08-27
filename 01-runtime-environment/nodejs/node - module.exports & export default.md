module.exports & export default 概念区别

module.exports 对象是由模块系统创建的，需要声明模块对外导出的内容，module.exports 则提供了暴露接口的方法，这种方法可以返回全局共享的变量或者方法

```
[案例]

// func.js
// 模块对外导出接口 module.exports
var func = {
  run: function() {}
}

module.exports = func

// app.js
// 导入接口, require
var func = require('./func.js');

func.run();
```

moudle.exports ，使用方法 moudle.exports= [function name]

exports , 使用方法 exports.[function name] = [function name] 

**exports ** 返回的是模块函数 ， **module.exports ** 返回的是模块对象本身，返回的是一个类 ；exports 的方法可以直接调用 ，module.exports需要new对象之后才可以调用 ；exports 只能对外暴露单个函数，但是module.exports却能暴露一个类。

exports是module.exports的一个引用，exports指向的是module.exports ，此时 moudle.exports.[function name]   = [function name]  是完全和  exports.[function name] = [function name]  相等的 ，通常还是推荐使用exports.[function name]，各司其职，代码逻辑清晰。

export、export default

```
require : node 和 es6 都支持的引入

export / import : 只有es6 支持的导出引入

module.exports / exports : 只有 node 支持的导出

// Node里面的模块系统遵循的是CommonJS规范
```

