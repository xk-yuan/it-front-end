    级联样式表 Cascading Style Sheet CC ，拥有对网页对象和模型样式编辑能力，并能够进行初步交互设计，是目前基于文本展示最优秀的表现设计语言，可以用它开发网页样式，但是没法用它编程。

   换句话说，CSS 基本上是设计师的工具，不是程序员的工具。

  但是自诞生以来，基本语法和核心机制一直没有本质上的变化，它的发展几乎全是表现力层面上的提升，而造成其天性上的不足。

  CSS 预处理器，是一种专门的编成语言，是为了解决CSS描述性语言的不足而产生的，其在CSS语言之上增加了编成语言的特性，使得CSS 更加简洁、适应性更强、可读性更佳，更易于代码的维护等诸多好处。这种编成语言编译生存的目标文件就是CSS文件。

## 一、简介

```
[CSS 预处理器 - CSS 预处理器技术已经非常的成熟]

  ：LESS

	：SASS(SCSS)

  ：Stylus
```

```
[特性]

	：文件切分
  
    # 传统方案就是CSS原生的@import指令，或在HTML中加载多个CSS文件，这些方案通常不能满足性能要求
    
    # CSS预处理器扩展了@import指令的能力，通过编译环节将切分后的文件重新合并为一个大文件

  ：模块化 # 文件切分的思路再向前推进一步，就是 “模块化”
  
    entry.styl
     ├─ base.styl
     │   ├─ normalize.styl
     │   └─ reset.styl
     ├─ layout.styl
     │   ├─ header.styl
     │   │   └─ nav.styl
     │   └─ footer.styl
     ├─ section-foo.styl
     ├─ section-bar.styl
     └─ ...
 
    # 树形的根结节一般称作 “入口文件”，树形的其它节点一般称作 “模块文件”。

    # 入口文件 entry.styl 在编译时会引入所需的模块，生成 entry.css，然后被页面引用
  
  ：选择符嵌套
  
    # 文件内部的代码组织方式，它可以让一系列相关的规则呈现出层级关系
    
    .nav {margin: auto /* 水平居中 */; width: 1000px; color: #333;}
        .nav li {float: left /* 水平排列 */; width: 100px;}
            .nav li a {display: block; text-decoration: none;}
            
    # 手工维护缩进关系，当上级选择符发生变化时，所有相关的下级选择符都要修改
    
    .nav
      margin: auto  // 水平居中
      width: 1000px
      color: #333
      li
          float: left  // 水平排列
          width: 100px
          a
              display: block
              text-decoration: none

    #  CSS 预处理语言中，嵌套语法可以很容易地表达出规则之间的层级关系，为单条声明写注释也很清晰易读
    
	：变量

    /* 原生 CSS 代码 */
    strong {
      color: #ff4466;
      font-weight: bold;
    }
    .notice {
      color: #ff4466;
    }
    
    // 用 Stylus 来写
		$color-primary = #ff4466
    strong
      color: $color-primary
      font-weight: bold
    .notice
      color: $color-primary

  ：运算
  
    # 变量让值有了意义，那么运算则可以让值和值建立关联
    
  ：函数
  
    # 常用的运算操作抽象出来，就得到了函数
    
  ：Mixins
  
	  # 作用是把重复的代码放到一个类当中，每次只要引用类名，就可以引用到里面的代码
    
    # 部分样式抽出，作为单独定义的模块，被很多选择器重复使用

```

```
[学习模块]

	：基本语法

	：嵌套语法

	：变量 『作用域』

	：@import

	：混入

	：继承

	：函数

	：逻辑控制

```

